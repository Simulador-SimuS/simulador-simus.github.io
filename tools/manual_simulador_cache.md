# Manual do Simulador de Cache — versão com localidade

Este manual acompanha o arquivo `simulador_cache_localidade.html`. A aplicação funciona diretamente no navegador, sem instalação e sem conexão com a internet. Permite estudar mapeamentos de cache, políticas de substituição e os efeitos da localidade nos acessos à memória.

## 1. Começar a usar

1. Abra `simulador_cache_localidade.html` no navegador.
2. Configure as linhas da cache, os bytes por linha, os bits de endereço, o mapeamento e a política de substituição.
3. Digite uma sequência de endereços ou escolha um perfil e clique em **Gerar sequência aleatória**.
4. Clique em **Iniciar Simulação** para examinar o primeiro acesso ou em **Modo turbo** para ver diretamente o resultado final.
5. Use **Anterior**, **Próximo** e o histórico para acompanhar os acessos.

Os botões de idioma alternam a interface entre português, inglês e espanhol.

## 2. Configuração da cache

| Campo | Valores e significado |
|---|---|
| Linhas da Cache (total) | 2, 4, 8, 16, 32, 64, 128 ou 256 linhas, somando todas as vias. |
| Bytes por Linha (bloco) | 1, 2, 4, 8, 16, 32 ou 64 bytes por bloco. |
| Bits de Endereço | Número inteiro entre 6 e 32. Define o espaço de memória endereçável. |
| Tipo de Mapeamento | Direto, completamente associativo ou associativo por conjunto com 2 ou 4 vias. |
| Política de Substituição | FIFO, LRU ou Aleatória. |

Cada endereço identifica um **byte**. A capacidade de dados é:

**Capacidade = total de linhas × bytes por linha.**

Por exemplo, 256 linhas de 64 bytes armazenam 16.384 bytes, ou **16 KiB de dados**. Esse valor não inclui TAGs nem os metadados de controle.

### Conjuntos e vias

| Mapeamento | Organização com 256 linhas |
|---|---|
| Direto (1 via) | 256 conjuntos de 1 linha |
| 2 vias | 128 conjuntos de 2 linhas |
| 4 vias | 64 conjuntos de 4 linhas |
| Completamente associativo | 1 conjunto de 256 linhas |

O total de linhas deve ser divisível pelo número de vias. Duas linhas totais, por exemplo, não permitem quatro vias.

### Bits do endereço

O endereço é decomposto em **TAG, índice do conjunto e deslocamento dentro do bloco**:

- Bits de deslocamento: `log₂(bytes por linha)`.
- Bits de índice: `log₂(número de conjuntos)`.
- Bits de TAG: `bits de endereço − bits de índice − bits de deslocamento`.

A configuração precisa ter bits de endereço suficientes para o índice e o deslocamento. Com 256 linhas de 64 bytes, o mínimo é 14 bits no mapeamento direto, 13 em duas vias e 12 em quatro vias. É permitido que a TAG tenha zero bits.

Com 32 bits, os endereços válidos vão de **0 a 4.294.967.295**, ou **0x00000000 a 0xFFFFFFFF**. Isso representa um espaço endereçável de 4 GiB; o simulador não aloca essa quantidade de memória.

## 3. Sequência de endereços

Digite endereços decimais ou hexadecimais com prefixo `0x`, separados por vírgulas. Exemplo:

```text
0, 1, 2, 3, 0x04, 0x08, 0x00
```

Use somente inteiros dentro do intervalo definido pelos bits de endereço. O limite é **1.000 endereços por sequência**, incluindo sequências digitadas manualmente.

Para gerar uma sequência, selecione o perfil, informe a região de trabalho quando aplicável e escolha um tamanho entre 1 e 1.000. O botão **Gerar sequência aleatória** substitui o conteúdo do campo, limpa a simulação anterior e preenche os endereços em hexadecimal. Você pode editá-los antes de simular.

### Perfis de geração

| Perfil | Comportamento |
|---|---|
| Uniforme | Cada acesso escolhe um endereço em toda a memória. A região de trabalho não se aplica. |
| Sequencial com saltos | Começa em um endereço aleatório. Depois, há 90% de chance de avançar um byte e 10% de saltar para um endereço aleatório de toda a memória. Ao ultrapassar o último byte, retorna ao endereço zero. |
| Repetição de laços | Começa em um ponto aleatório da região e percorre seus bytes em sequência, retornando ao início da região ao chegar ao fim. |
| Região quente | Há 80% de chance de escolher um byte dentro da região e 20% de escolher um byte fora dela. Se a região ocupar toda a memória, a geração é uniforme. |
| Misto com localidade | Começa na região. Depois, há 60% de chance de avançar um byte na região, 30% de reutilizar um dos últimos 32 acessos e 10% de saltar para qualquer endereço da memória. |

Os percentuais são probabilidades por acesso, não quotas exatas. Repetir a geração pode produzir resultados diferentes.

No perfil Misto, quando o endereço anterior está fora da região, a opção de avanço sequencial retorna ao endereço zero. A reutilização considera os acessos recentes já gerados, inclusive os que ocorreram fora da região; no início, usa apenas os acessos disponíveis.

### Região de trabalho

A região começa sempre no endereço **zero**. Uma região de 64 bytes abrange os endereços de 0 a 63. Seu tamanho pode variar de 1 byte até o tamanho da memória endereçável.

- Região menor que a cache: favorece a permanência dos blocos e os acertos após o carregamento inicial.
- Região maior que a cache: ajuda a observar substituições e diferenças entre políticas.
- Memória muito grande com geração uniforme: tende a gerar pouca reutilização, reduzindo os acertos.

Uma região pequena não garante acertos: os primeiros carregamentos, os conflitos de mapeamento e os acessos externos também influenciam o resultado. A interface informa a capacidade da cache e o tamanho da memória para facilitar a escolha.

## 4. Controles da simulação

| Botão | Ação |
|---|---|
| Iniciar Simulação | Calcula a sequência e exibe o primeiro passo. |
| Modo turbo | Calcula a sequência sem exibir passos intermediários e atualiza a tela com o último passo e as estatísticas finais. |
| Anterior / Próximo | Navega entre os passos já calculados. |
| Auto | Inicia ou pausa a apresentação automática, com intervalo de 1,5 segundo. |
| Resetar | Limpa os resultados e interrompe a apresentação automática. Mantém a sequência e os campos de configuração. |

Depois de usar o turbo, é possível voltar aos passos anteriores. Os contadores passam a representar o trecho da sequência até o passo exibido. Para aplicar alterações na sequência ou na configuração, inicie uma nova simulação.

## 5. Interpretar os resultados

- **Cache HIT:** o bloco solicitado já estava presente no conjunto correspondente.
- **Cache MISS:** o bloco não estava presente e precisou ser carregado.
- **Taxa de acerto:** quantidade de hits dividida pelo total de acessos até o passo exibido.
- **Write-backs:** número de substituições de blocos sujos até o passo exibido.

O painel do passo identifica o acesso e seu resultado. O painel de decomposição mostra o endereço e seus campos. A **TAG aparece em hexadecimal, com prefixo `0x`**, tanto na decomposição quanto na tabela da cache; a decomposição também conserva a representação binária. Zeros à esquerda acomodam a quantidade de bits de TAG. Quando não há bits de TAG, seu campo é omitido da decomposição.

A TAG é a parte superior do endereço, e não o endereço completo. Índice e deslocamento continuam apresentados separadamente.

### Tabela da cache

| Coluna | Significado |
|---|---|
| Conjunto | Conjunto ao qual a linha pertence. |
| Linha | Posição dentro do conjunto, começando em zero. |
| Válido | 1 indica bloco presente; 0 indica linha ainda vazia. |
| Sujo | D indica bloco modificado; um traço indica bloco limpo. |
| Tag | Identificador do bloco em hexadecimal. Um traço indica linha inválida. |
| Dados | Representação ilustrativa do endereço que carregou a linha. Não mostra todos os bytes do bloco. |
| Último Uso / Tempo Carga | Informação usada pela política LRU ou FIFO, respectivamente. |

### Políticas de substituição

Linhas inválidas são utilizadas primeiro. Quando o conjunto está cheio:

- **FIFO:** substitui a linha carregada há mais tempo.
- **LRU:** substitui a linha que está há mais tempo sem acesso.
- **Aleatória:** sorteia uma linha do conjunto.

No mapeamento direto, existe apenas uma linha por conjunto; por isso, a política não muda a escolha da vítima.

## 6. Experimento sugerido

1. Configure 8 linhas, 4 bytes por linha, 8 bits de endereço, mapeamento direto e FIFO. A cache terá 32 bytes.
2. Gere 1.000 acessos com perfil Uniforme e execute em modo turbo. Anote a taxa de acerto.
3. Escolha Misto, região de 64 bytes, gere outra sequência e repita.
4. Experimente Repetição de laços com regiões de 16, 32 e 64 bytes.
5. Para comparar mapeamentos e políticas, mantenha a mesma sequência no campo e altere apenas a configuração desejada.

Registre também o tamanho dos blocos, a capacidade da cache e o perfil: a taxa de acerto isolada não descreve todo o experimento.

## 7. Limites do modelo e cuidados na comparação

O simulador é didático. Não modela latência, ciclos de processador, níveis L1/L2/L3, prefetch, coerência entre processadores nem o conteúdo completo da memória.

Não há distinção explícita entre operações de leitura e escrita na sequência. O simulador marca aleatoriamente uma linha como suja: aproximadamente 30% nos carregamentos e 50% nos hits. Uma linha já suja permanece assim até ser substituída. Portanto, o total de write-backs pode variar entre execuções com os mesmos endereços.

O gerador e a política de substituição aleatória não possuem semente configurável. Para repetir a sequência, copie seu texto antes de gerar outra. FIFO e LRU mantêm os resultados de hit/miss para a mesma sequência e configuração; a política Aleatória pode produzir resultados diferentes.

Se aparecer uma mensagem de configuração inválida, confira os bits de endereço, o total de linhas e o número de vias. Se a região exceder a memória, reduza seu tamanho ou aumente os bits de endereço.
