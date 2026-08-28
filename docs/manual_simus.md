# SimuS
## Simulador do Processador Sapiens
### Manual de Utilização

---

## 1. Introdução

O SimuS (Simulador Sapiens) é uma ferramenta educacional desenvolvida para simular o funcionamento do processador Sapiens. Este simulador permite aos estudantes escrever, compilar e executar programas em linguagem de montagem, visualizando em tempo real o comportamento do processador, registradores, flags e memória.

O SimuS oferece recursos avançados de depuração, incluindo execução passo a passo, breakpoints, visualização de memória e portas de entrada/saída simuladas.

---

## 2. Interface do Usuário

A linguagem da interface de usuário pode ser selecionada para português, inglês ou espanhol clicando-se em uma das bandeiras no canto superior da janela principal.

A interface do SimuS está dividida em três painéis principais, cada um com funções específicas para facilitar o desenvolvimento e depuração de programas.

### 2.1. Painel Esquerdo - Editor e Execução

Este painel contém três abas que permitem editar código, visualizar erros e acompanhar a execução:

#### 2.1.1. Aba Editor

Área de edição de código em linguagem de montagem com as seguintes características:

- Editor de texto com destaque de sintaxa para código em linguagem de montagem
- Fundo escuro para reduzir fadiga visual durante programação
- Fonte monoespaçada (Consolas) para melhor alinhamento do código
- Suporte a comentários (linhas iniciadas com ponto e vírgula ;)

#### 2.1.2. Aba Erros

Exibe mensagens de erro geradas durante a compilação:

- Lista todos os erros encontrados no código fonte
- Cada erro mostra a linha e uma descrição do problema
- Clique em um erro para posicionar o cursor na linha correspondente no editor
- Indicador vermelho no título da aba mostra o número de erros encontrados

#### 2.1.3. Aba Execução

Visualização do código compilado com recursos de depuração:

- Exibe o código em linguagem de montagem com endereços de memória em hexadecimal
- Destaque em amarelo na linha atual de execução (PC - Program Counter)
- Rótulos (*labels*) exibidos em cor laranja para fácil identificação
- Clique em qualquer linha para adicionar/remover breakpoint (marcado em vermelho no endereço)
- Rolagem automática para acompanhar a execução do programa

### 2.2. Painel Central - CPU e Controles

Este painel concentra todos os controles de execução e visualização do estado da CPU:

#### 2.2.1. Botões de Controle

Cinco botões com cores distintas para controlar a execução:

- **Passo (Laranja):** Executa uma única instrução e para. Ideal para depuração detalhada.
- **Executar (Verde):** Executa o programa continuamente em velocidade normal (50ms por instrução). Para automaticamente em *breakpoints* ou ao encontrar a instrução `HLT`.
- **Turbo (Rosa):** Executa o programa em alta velocidade (1000 instruções por ciclo). Útil para programas longos. Também respeita *breakpoints*.
- **Parar (Vermelho):** Interrompe a execução em qualquer modo (Executar ou Turbo).
- **Reset (Preto):** Reinicia o processador ao estado inicial após uma instrução `HLT`. Restaura PC, registradores e portas de E/S, mas preserva o conteúdo da memória.

#### 2.2.2. Barra de Status

Exibe o estado atual do simulador em texto cinza, abaixo dos botões de controle. Mensagens incluem: *"Pronto"*, *"Executando..."*, *"TURBO - Executando..."*, *"HALT - Programa Finalizado"*, entre outras.

#### 2.2.3. Registradores

Três caixas exibindo os valores dos registradores principais em hexadecimal:

- **AC (Acumulador):** Registrador de 8 bits usado para operações aritméticas e lógicas (formato: XX)
- **PC (Program Counter):** Registrador de 16 bits que aponta para o endereço da próxima instrução (formato: XXXX)
- **SP (Stack Pointer):** Registrador de 16 bits que aponta para o topo da pilha (formato: XXXX, com valor inicial em FFFF)

#### 2.2.4. Instrução Atual

Caixa com fundo escuro exibindo o mnemônico da instrução atualmente apontada pelo PC. Exemplo: `LDA #0xFF`. Esta visualização em destaque amarelo-dourado facilita o acompanhamento da execução.

#### 2.2.5. Flags (Sinalizadores)

Três indicadores visuais que mostram o estado dos flags do processador:

- **N (Negativo):** Acende em azul quando o resultado da última operação é negativo (bit 7 = 1)
- **Z (Zero):** Acende em azul quando o resultado da última operação é zero
- **C (Carry):** Acende em azul quando há overflow/carry na última operação aritmética

#### 2.2.6. Portas de Entrada/Saída

Interface simulada de periféricos com quatro componentes:

- **Banner - Texto:** *Display* de texto largo que exibe caracteres ASCII enviados pela instrução `OUT 3`. Suporta múltiplas linhas e texto bidirecional. Exemplo: *"Sapiens 2.0"*.
- **Entrada (IN) - Hex/Bin:** Campo de texto onde o usuário digita valores hexadecimais (00-FF) ou binários (8 bits) que serão lidos pela instrução `IN 0`. Pressione `ENTER` após digitar para confirmar o valor. Um LED verde acende quando há dado disponível.
- **Saída (OUT) - Hex/Bin:** Display hexadecimal/binário que mostra o último valor enviado pela instrução `OUT 0`. Formato: XX ou XXXXXXXX.
- **LED de Status:** Indicador verde que acende quando há dado digitado e confirmado na entrada, disponível para leitura via `IN 1` (porta de *status*).

### 2.3. Painel Direito - Visualização da Memória

Exibe o conteúdo da memória RAM em formato hexadecimal com navegação:

#### 2.3.1. Barra de Navegação

Controles no topo do painel de memória:

- **Botão ‹ (Anterior):** Retrocede 256 bytes (32 linhas) na visualização
- **Campo de Endereço:** Caixa de texto central mostrando o endereço inicial da visualização em hexadecimal (formato: XXXX). Você pode digitar um endereço e pressionar ENTER para navegar diretamente.
- **Botão › (Próximo):** Avança 256 bytes (32 linhas) na visualização.
- **Botão < (Anterior):** Recua 256 bytes (32 linhas) na visualização.
- **Botão PC:** Navega automaticamente para o endereço atual do Program Counter, centralizando a visualização na instrução sendo executada.
- - **Botão SP:** Navega automaticamente para o endereço atual do Stack Pointer, centralizando a visualização na pilha do programa.

#### 2.3.2. Grade de Memória

Visualização em grade hexadecimal com as seguintes características:

- Exibe 32 linhas de 8 bytes cada (256 bytes totais por tela)
- Coluna da esquerda mostra o endereço base de cada linha em hexadecimal
- Cabeçalho superior indica o offset (+0 a +7) para cada coluna
- Bytes com valor 00 são exibidos em cinza claro para facilitar identificação
- Byte apontado pelo PC é destacado com fundo amarelo
- Byte apontado pelo SP é destacado com fundo lilás 
- Fonte monoespaçada garante alinhamento perfeito dos valores

---

## 3. Barra de Ferramentas de Arquivo

Localizada no topo do painel esquerdo, oferece botões para gerenciamento de arquivos e janelas auxiliares:

- **📂 Abrir:** Abre um arquivo do disco (.txt, .asm, .sap). O conteúdo é carregado no editor, substituindo o código atual. O nome do arquivo é exibido na aba **Editor**.
- **💾 Salvar Como...:** Salva o código atual do editor em um arquivo no disco. Abre diálogo do navegador para escolher o nome e local. Extensão padrão: .asm.
- **✔ Compilar:** Compila o código em linguagen de montagem no editor. Se houver erros, a aba **Erros** é ativada automaticamente com a lista de problemas. Se a compilação for bem-sucedida, o código compilado é carregado na memória e a aba Execução é exibida. O PC é posicionado no endereço definido pela diretiva ORG.
- **Terminal:** Mostra ou esconde a janela *pop-up* da console de texto. A janela pode ser movida arrastando sua barra de título.
- **Video:** Mostra ou esconde a janela *pop-up* do display gráfico virtual. A janela também pode ser movida pela barra de título.

### 3.1. Janelas Pop-up

O Terminal e o Video são janelas flutuantes independentes. Para reposicioná-las, clique e arraste a barra superior da janela. O botão circular vermelho na barra de título fecha/esconde a janela.

---

## 4. Fluxo de Trabalho Típico

Siga estes passos para desenvolver e executar programas no SimuS:

1. **Editar o Código:** Na aba **Editor**, escreva seu programa em linguagem de montagem. Use comentários (;) para documentar o código. Lembre-se de incluir a diretiva `ORG` para definir o endereço inicial e `END` para marcar o fim do programa.

2. **Compilar:** Clique no botão `✔ Compilar`. Se houver erros, corrija-os conforme indicado na aba **Erros** e compile novamente.

3. **Definir Breakpoints (Opcional):** Na aba **Execução**, clique nas linhas onde deseja pausar a execução. Um círculo vermelho aparecerá no endereço.

4. **Executar:** Escolha um modo de execução:
   - Passo: Para depuração detalhada, instrução por instrução
   - Executar: Para velocidade normal, com visualização
   - Turbo: Para programas longos, execução máxima

5. **Acompanhar a Execução:** Observe os registradores, *flags*, memória e portas de E/S sendo atualizados em tempo real. A linha atual é destacada em amarelo na aba **Execução**.

6. **Interagir com E/S:** Quando o programa executar `IN 0`, digite um valor hexadecimal no campo Entrada (Hex) e pressione `ENTER`. Valores enviados via OUT são exibidos automaticamente.

7. **Finalizar:** O programa para automaticamente ao encontrar a instrução `HLT`. Use o botão `RESET` para reiniciar e executar novamente.

8. **Salvar:** Use 💾 Salvar Como... para guardar seu trabalho em arquivo.

---

## 5. Conjunto de Instruções Sapiens

O processador Sapiens implementa as seguintes categorias de instruções:

### 5.1. Instruções de Transferência de Dados

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| LDA | Load Accumulator | Carrega AC com valor da memória ou imediato |
| STA | Store Accumulator | Armazena AC na memória |
| LDS | Load Stack Pointer | Carrega SP com valor de 16 bits |
| STS | Store Stack Pointer | Armazena SP na memória (16 bits) |

### 5.2. Instruções Aritméticas

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| ADD | Addition | AC = AC + operando (atualiza flags) |
| ADC | Add with Carry | AC = AC + operando + C (atualiza flags) |
| SUB | Subtraction | AC = AC - operando (atualiza flags) |
| SBC | Subtract with Carry | AC = AC - operando - C (atualiza flags) |

### 5.3. Instruções Lógicas

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| AND | Logical AND | AC = AC & operando (atualiza flags) |
| OR | Logical OR | AC = AC \| operando (atualiza flags) |
| XOR | Exclusive OR | AC = AC ^ operando (atualiza flags) |
| NOT | Logical NOT | AC = ~AC (atualiza flags) |

### 5.4. Instruções de Deslocamento

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| SHL | Shift Left | Desloca AC 1 bit à esquerda (bit 0 = 0, C recebe bit 7) |
| SHR | Shift Right | Desloca AC 1 bit à direita lógico (bit 7 = 0, C recebe bit 0) |
| SRA | Shift Right Arithmetic | Desloca AC 1 bit à direita aritmético (mantém bit 7) |

### 5.5. Instruções de Controle de Fluxo

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| JMP | Jump | Salta incondicionalmente para endereço |
| JZ | Jump if Zero | Salta se flag Z = 1 |
| JNZ | Jump if Not Zero | Salta se flag Z = 0 |
| JN | Jump if Negative | Salta se flag N = 1 |
| JP | Jump if Positive | Salta se flag N = 0 |
| JC | Jump if Carry | Salta se flag C = 1 |
| JNC | Jump if No Carry | Salta se flag C = 0 |

### 5.6. Instruções de Sub-rotina

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| JSR | Jump to Subroutine | Salva PC na pilha e salta para sub-rotina |
| RET | Return | Retorna de sub-rotina (recupera PC da pilha) |

### 5.7. Instruções de Pilha

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| PUSH | Push to Stack | Empilha AC (mem[SP] = AC, depois SP--) |
| POP | Pop from Stack | Desempilha para AC (SP++, depois AC = mem[SP]) |

### 5.8. Instruções de Entrada/Saída

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| IN | Input | Lê dado da porta especificada para AC |
| OUT | Output | Envia AC para porta especificada |

#### Portas de E/S Disponíveis:

| Instrução | Função |
|-----------|--------|
| IN 0 | Lê valor hexadecimal digitado pelo usuário |
| IN 1 | Lê status da entrada (1 = dado disponível, 0 = sem dado) |
| OUT 0 | Envia AC para display hexadecimal de saída |
| OUT 2 | Limpa o banner de texto |
| OUT 3 | Envia caractere ASCII para banner de texto (adiciona ao final) |

### 5.9. Instruções Especiais

| Mnemônico | Nome | Descrição |
|-----------|------|-----------|
| NOP | No Operation | Não faz nada (pode ser usado para timing) |
| HLT | Halt | Para a execução do processador |
| TRAP | Trap | Gera chamada de serviço |


#### Operações de TRAP Disponíveis:

- O número do TRAP é passado no acumulador. Parâmetros adicionais são passados no endereço de memória do operando.
- A instrução `TRAP` devolve códigos de resultado no acumulador, mas não atualiza as flags. Antes de testar o retorno com `JZ` ou `JNZ`, use uma instrução que atualize flags sem alterar o valor, como `OR #0`:

```asm
LDA #20
TRAP VIDEO_CONFIG
OR #0
JNZ ERRO
```

| Instrução | Função |
|-----------|--------|
| #0 | Limpa o terminal da console |
| #1 | Lê caractere do terminal e salva no acumulador e endereço de memória do operando.|
| #2 | Escreve um caractere do endereço de memória do operando no terminal. |
| #3 | Lê uma cadeia de caracteres do terminal e salva no endereço de memória do operando. |
| #4 | Escreve uma cadeia de caracteres a partir do endereço operando (até achar um NULL) |
| #5 | Delay (Aguarda de 0 a 65535 ms) |
| #6 | Beep (Sintetizador de Áudio). Recebe a frequência e duração como parâmetros |
| #7 | Retorna um número pseudo-aleatório entre 0 e 99 no acumulador. |
| #20 | Configura o *display* gráfico virtual. O operando aponta para um bloco `DW base`, onde `base` é o início da memória de vídeo. |
| #21 | Limpa a memória de vídeo com uma cor. O operando aponta para `DB cor`. |
| #22 | Desenha um pixel. O operando aponta para `DB x, y, cor`. |
| #23 | Desenha uma reta. O operando aponta para `DB x0, y0, x1, y1, cor`. |
| #24 | Desenha um retângulo. O operando aponta para `DB x, y, largura, altura, cor, preenchido`. |
| #25 | Desenha um círculo. O operando aponta para `DB cx, cy, raio, cor, preenchido`. |

#### Display Gráfico Virtual

O *display* gráfico virtual tem resolução de 128 × 64 pixels. A memória de vídeo ocupa 8192 bytes consecutivos, com 1 byte por pixel. A `TRAP #20` define qual trecho da memória de 64 KB será usado como área de vídeo. O endereço base deve estar alinhado em múltiplo de 256 e a área `base + 8192` não pode ultrapassar o limite da memória.

O layout dos pixels é linear:

```text
endereço = base + (y * 128) + x
```

As cores usam o formato de 8 bits `RRRGGGBB`:

| Valor | Cor aproximada |
|-------|----------------|
| `224` / `0xE0` | Vermelho |
| `28` / `0x1C` | Verde |
| `3` / `0x03` | Azul |
| `252` / `0xFC` | Amarelo |
| `255` / `0xFF` | Branco |

Retornos principais da `TRAP #20`:

| AC | Significado |
|----|-------------|
| 0 | Sucesso |
| 1 | Endereço base não alinhado em 256 bytes |
| 2 | A área de vídeo ultrapassa o limite da memória |
| 4 | Usado pelas TRAPs gráficas quando o vídeo ainda não foi configurado |

---

## 6. Modos de Endereçamento

O Sapiens suporta quatro modos de endereçamento, identificados pelos 2 bits mais significativos do opcode:

| Bits | Modo | Exemplo | Operação | Descrição |
|------|------|---------|----------|-----------|
| 00 | Direto | `LDA 50` | `AC = mem[50]` | O operando é o endereço na memória do dado|
| 01 | Indireto | `LDA @50` | `AC = mem[mem[50]]` | O operando aponta para endereço que contém o endereço final do dado|
| 10 | Imediato 8 bits | `LDA #10` | `AC = 10` | O operando é o byte seguinte à instrução |
| 11 | Imediato 16 bits| `LDS #1000` | `SP = 1000` | O operando são os dois bytes seguintes à instrução |

### Observações sobre Endereçamento:

- Instruções sem operando (NOP, RET, PUSH, POP, etc.) ignoram o modo de endereçamento
- O uso do prefixo `@` no operando indica modo indireto, `#` indica o modo imediato, a ausência indica o modo direto

---

## 7. Formato dos operandos

O Sapiens suporta vários tipos de formatos para os operando das instruçõoes:

- Decimal: 10 - O número sem decoradores
- Binário: 0b01010101 ou 01010101B
- Hexadecimal: 0x05 ou 05H (tem começar com digito numérico)

## 8. Diretivas do Montador

O montador do SimuS reconhece as seguintes diretivas:

| Diretiva | Descrição | Exemplo | Efeito |
|----------|-----------|---------|--------|
| `ORG endereço` | Define o endereço inicial do programa | `ORG 0` | Programa inicia no endereço 0 |
| `END` | Marca o fim do código fonte | `END` | Última linha do arquivo |
| `DB valor[, valor...]` | Define um ou mais bytes (8 bits) | `DB 0xFF, 10, 1010B` | Armazena a lista de bytes na memória |
| `DW valor[, valor...]` | Define uma ou mais words (16 bits) | `DW 0x1234, 1000` | Armazena words em *little-endian* |
| `DS quantidade` | Define espaço (reserva bytes) | `DS 10` | Reserva 10 bytes zerados |
| `LABEL EQU valor` | Define uma constante | `TESTE EQU 10` | TESTE será igual 10 |

> **Atenção:** para constantes, use `LABEL EQU valor` sem dois pontos. A forma `LABEL: EQU valor` cria primeiro um rótulo no endereço atual e pode não definir a constante como esperado.
>

### Uso de Rótulos (Labels):

Rótulos podem ser definidos antes de qualquer instrução ou diretiva, terminando com dois pontos:

```assembly
LOOP:
    LDA VALOR
    JNZ LOOP
```

- Rótulos devem começar com letra e podem conter letras, números e underscore
- São automaticamente convertidos para maiúsculas pelo montador
- Podem ser usados como operandos em instruções de salto e acesso à memória
- É possível usar `ROTULO+deslocamento` para acessar bytes seguintes ao rótulo. O deslocamento aceito atualmente vai de 1 a 8. Por exemplo, se `PALAVRA: DW 0x1234`, então `PALAVRA` aponta para o byte baixo (`0x34`) e `PALAVRA+1` aponta para o byte alto (`0x12`).

---

## 9. Exemplos de Programas

### 9.1. Eco Simples

Programa que aguarda entrada do usuário e ecoa o valor:

```assembly
; Programa de Eco
ORG 0
LOOP:
    IN 1          ; Lê status
    OR #0         ; Verifica o valor lido
    JZ LOOP       ; Aguarda dado eqto for 0 
    IN 0          ; Lê valor
    OUT 0         ; Exibe valor
    HLT
END
```

### 9.2. Contador de 0 a 9

Conta de 0 a 9 e para:

```assembly
; Contador
ORG 0
LOOP:
    LDA CONT      ; Carrega o valor do contador
    OUT 0         ; Mostra valor
    ADD #1        ; Incrementa 
    STA CONT      ; Armazena o novo valor
    SUB #10       ; Compara com 10
    JNZ LOOP      ; Continua se != 10
    HLT
END
CONT:   DB 0;
```

### 9.3. Sub-rotina com Pilha

Demonstra passagem de parâmetro pela pilha. O programa principal empilha o
parâmetro antes de chamar a sub-rotina. Como `JSR` também empilha o endereço de
retorno, a sub-rotina primeiro salva esse endereço em uma variável `DW`, depois
retira o parâmetro, calcula o resultado e restaura o endereço de retorno para
que `RET` funcione corretamente.

```assembly
; Passagem de parâmetro pela pilha
; Resultado retornado no acumulador

ORG 0
    LDA #42          ; Parâmetro da sub-rotina
    PUSH             ; Empilha o parâmetro
    JSR DOBRO        ; JSR empilha o endereço de retorno
    OUT 0            ; Mostra o resultado: 84
    HLT

DOBRO:
    ; Ao entrar na sub-rotina, o topo da pilha contém
    ; o endereço de retorno colocado por JSR.
    ; Abaixo dele está o parâmetro empilhado pelo programa principal.

    POP              ; Byte baixo do endereço de retorno
    STA RET
    POP              ; Byte alto do endereço de retorno
    STA RET+1
    POP              ; Recupera o parâmetro
    STA PARAM
    ; Calcula PARAM * 2
    LDA PARAM
    ADD PARAM
    STA RESULT

    ; Restaura o endereço de retorno.
    ; RET desempilha primeiro o byte baixo e depois o byte alto.
    ; Como PUSH empilha e decrementa SP, empilhamos primeiro o byte alto.
    LDA RET+1
    PUSH
    LDA RET
    PUSH
    LDA RESULT       ; Retorna o resultado no acumulador
    RET

RET:    DW 0         ; Endereço de retorno salvo pela sub-rotina
PARAM:  DB 0         ; 
RESULT: DB 0

END 0
```
---

### 9.4. Display Gráfico Virtual

Configura a memória de vídeo em `0x4000`, limpa a tela, desenha um retângulo preenchido, uma reta e um círculo:

```assembly
ORG 0

MAIN:
    LDA #20
    TRAP VIDEO_CONFIG
    OR #0
    JNZ ERRO
    LDA #21
    TRAP LIMPAR
    LDA #24
    TRAP RETANGULO
    LDA #23
    TRAP RETA
    LDA #25
    TRAP CIRCULO
    HLT
ERRO:
    HLT

VIDEO_CONFIG:
    DW VIDEO_BASE
LIMPAR:
    DB 3              ; azul
RETANGULO:
    DB 48, 16, 32, 32, 224, 1
RETA:
    DB 0, 63, 127, 0, 28
CIRCULO:
    DB 64, 32, 18, 252, 0

VIDEO_BASE EQU 16384 ; 0x4000

END MAIN
```

---

## 10. Resolução de Problemas Comuns

### Erro: "Instrução Inválida"
- Verifique se o mnemônico está escrito corretamente. Lembre-se que o montador não diferencia maiúsculas de minúsculas.

### Erro: "Rótulo Não Definido"
- Certifique-se de que o rótulo usado na instrução foi definido em algum lugar do código com dois pontos (:).

### Programa não executa após compilar
- Verifique se você clicou em Compilar antes de tentar executar. A luz verde de status deve mostrar "Carregado" na mensagem.

### Breakpoint não funciona
- Breakpoints só funcionam em linhas com instruções executáveis. Linhas vazias, comentários e diretivas não podem ter breakpoints.

### Memória não atualiza durante execução
- No modo Turbo, a interface não atualiza a cada instrução para manter velocidade máxima. Use modo Executar ou Passo para ver mudanças em tempo real.

### IN não lê o valor digitado
- Lembre-se de pressionar ENTER após digitar o valor hexadecimal. O LED verde deve acender indicando que o dado está pronto.

### Display gráfico não mostra desenho
- Verifique se o programa executou `TRAP #20` antes das demais TRAPs gráficas.
- Após `TRAP #20`, use `OR #0` ou `SUB #0` antes de `JZ/JNZ` para testar corretamente o valor retornado em AC.
- A base da memória de vídeo deve ser múltiplo de 256. Um valor recomendado é `0x4000` (`16384`).
- Use `VIDEO_BASE EQU 16384` sem dois pontos para definir a constante.
- Clique no botão **Video** se a janela não estiver visível.

---

## 11. Dicas e Boas Práticas

- **Use comentários generosamente:** Documente o propósito de cada seção do código com linhas iniciadas por ponto e vírgula (;).
- **Organize com rótulos:** Use nomes descritivos para rótulos (LOOP, INICIO, FIM, CALCULAR, etc.) para tornar o código mais legível.
- **Teste incrementalmente:** Compile e teste pequenas partes do programa antes de adicionar mais funcionalidades.
- **Use breakpoints estrategicamente:** Coloque *breakpoints* em pontos críticos (início de laços, chamadas de sub-rotinas, decisões) para facilitar depuração.
- **Monitore os flags:** Observe as *flags* `N`, `Z` e `C` durante execução para entender como as operações afetam o estado do processador.
- **Sempre termine com HLT:** Garanta que todo caminho de execução termine com `HLT` para evitar comportamento imprevisível.
- **Salve seu trabalho frequentemente:** Use o botão `💾 Salvar Como...` regularmente para não perder progresso.
- **Verifique a aba Memória:** Durante depuração, use o botão `PC` para navegar rapidamente até a instrução atual na visualização de memória.

---

## 12. Conclusão

O SimuS é uma ferramenta completa para aprendizado de arquitetura de computadores e programação em linguagem de montagem. Através de sua interface intuitiva e recursos avançados de depuração, estudantes podem experimentar conceitos fundamentais como:

- Ciclo de busca-decodificação-execução
- Funcionamento de registradores e flags
- Organização da memória
- Pilha e chamadas de sub-rotinas
- Entrada e saída de dados
- Diferentes modos de endereçamento

Este manual cobre os aspectos essenciais do simulador. Para questões adicionais ou suporte técnico, consulte a documentação do processador Sapiens ou entre em contato com o desenvolvedor.

**Bons estudos e boa programação!**
