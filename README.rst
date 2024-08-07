Simulador SimuS
===============

O SimuS é um simulador desenvolvido para o processador didático Sapiens,
detalhado no livro *Arquitetura de Computadores - Uma Introdução*
(Editora LTC - 2024). Este livro é fruto da vasta experiência dos
autores ao longo de anos ministrando cursos de graduação em áreas
tecnológicas. Sua missão é apresentar, de maneira acessível, o
funcionamento dos computadores a alunos de disciplinas de Organização ou
Arquitetura de Computadores, abrangendo cursos como Bacharelado em
Ciência da Computação, Engenharia de Computação, Bacharelado em Sistemas
de Informação, Licenciatura em Computação, Cursos Superiores de
Tecnologia e, mais recentemente, Ciência de Dados.

O uso de exemplos de programas em linguagem de montagem é enfatizado
como crucial para a compreensão, e para isso, é disponibilizado um
simulador didático gratuito no repositório `Simulador
Simus <https://github.com/Simulador-Simus/SimuS>`__, contendo
código-fonte, executáveis para diversos sistemas operacionais e um
manual detalhado. Além disso, todos os exemplos em linguagem de montagem
utilizados no livro e respostas para os exercícios propostos no Capítulo
de Linguagem de Montagem estão disponíveis no mesmo repositório.

No simulador SimuS mantivemos a interface básica do seu predecessor, o
simulador Neanderwin, mas com o acréscimo de algumas funcionalidades.
Desde o início do projeto nosso objetivo era facilitar ao máximo as
atividades didáticas do professor e o apoio mais completo possível para
as dificuldades comuns do aluno. Para isso foi disponibilizado um
ambiente integrado para desenvolvimento, com versões para os sistemas
operacionais Windows e Linux, com os seguintes módulos: - Editor de
textos integrado, que possibilita a abertura, edição e salvamento de
arquivos em linguagem de montagem. - Montador (assembler) também
integrado, gerando o código objeto final em linguagem de montagem.
Possui compatibilidade com programas escritos para os processadores
Neander ou Neander-X. - Simulador da arquitetura, com possibilidade,
além da visualização, de modificação dos elementos arquiteturais do
processador, tais como registrador de instrução, apontador de instrução,
apontador de pilha, acumulador, flags N, Z e C; além da execução
passo-a-passo ou direta. - Módulo de depuração, definindo pontos de
parada e variáveis em memória para serem monitoradas, em caso de mudança
de valor a execução é interrompida. - Visualização e modificação da
memória simulada, no formato hexadecimal os endereços e também para seu
conteúdo, agora expandida para 64 Kbytes. - Ferramenta de apoio ao
aprendizado de instruções, com ajuda integrada ao editor de textos, para
a geração de código em linguagem de montagem do processador Sapiens. -
Utilitário para conversão de bases binária, decimal e hexadecimal. -
Simulador de dispositivos de E/S, que inclui os tradicionais painel com
8 chaves e visor hexadecimal, além de um teclado de 12 teclas e um
“banner” de 16 linhas. Estes dispositivos são acessados no espaço de
endereçamento de E/S convencional com as instruções IN e OUT. -
Dispositivos especiais como uma console virtual, acessada pelo mecanismo
de TRAP descrito em detalhes na documentação. Com esse mecanismo outros
módulos mais complexos possam ser facilmente instalados, sem necessidade
de expor esta complexidade para osusuários. - Gerador/carregador de
imagem da memória simulada, podendo ser salva em formato hexadecimal.
Note que neste caso a compatibilidade entre o Simus e o Neanderwin não é
mantida, ou seja, a imagem salvaem um simulador não pode ser carregada
em outro.

Um dos recursos disponíveis no repositório é um `manual <./simus.pdf>`__
para a arquitetura do processador Sapiens, cujo modelo de arquitetura
pode ser visalizado a seguir:

Ao longo do tempo diversos acréscimos foram feitos ao simulador SimuS,
entre os quais destacamos:

-  A possibilidade de controlar, via interface USB, atuadores e sensores
   conectados aos pinos Arduino, com uso do protocolo Firmata.

-  Uma versão para uso no Raspberry Pi, permitindo o controle de
   sensores e atuadores conectados via GPIO.

-  Uma versão em python, para uma extensão com acumulador de 16 bits.

   Em breve estarão disponíveis no repositório alguns slides de apoio
   para o material do livro.
