---
title: Ferramentas, Compiladores e Ambientes de Desenvolvimento
sidebar_position: 1
slug: /c-lang-tools
---


Aqui pessoal vamos analisar algumas ferramentas e o processo de compilação de código.

## 1. Origem da compilação de código

Vamos avaliar algumas coisas antes de iniciarmos nosso estudo. Primeiro vamos compreender como os programas de computador são criados e executados por nossas máquinas. Primeiro, nosso processador é uma máquina capaz de compreender um conjunto de instruções, chamadas de código de máquina. Essas instruções são responsáveis por executar operações a nível do processador, como ler e escrever em posições de memória, mover dados entre registradores, realizar operações aritméticas e lógicas, para citar algumas.


:::tip[Como os processadores compreendem as instruções]

<iframe width="560" height="315" src="https://www.youtube.com/embed/vqs_0W-MSB0?si=qHdCGD0GVPTBPcvJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

> "Murilão, beleza, até aqui você falou bonito, deu para compreender que o processador compreende um conjunto de instruções e executa umas operações. Mas onde a programação entre ai?"

Ótima pergunta! Vamos avaliar onde nossos programas entre nessa história toda. O processador carrega as instruções e os operandos dessas instruções de endereços de memória. Agora, nossos programas são responsáveis por fornecer essas instruções e operandos. Para isso vamos verificar algumas formas de fazer isso.

Primeiro, as pessoas programadoras faziam seus programas em cartões perfurados, isso em 1800, la na industria têxtil. Cada um dos furos dizia para os teares programáveis onde eles deveriam fazer os pontos de costura, os cartões eram lidos e interpretados pelo tear.

<img src="https://www.stylourbano.com.br/wp-content/uploads/2017/02/TEAR-JACQUARD-min.jpg" alt="Cartões perfurados na industria têxtil" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />>
<br />

Deste princípio, em 1840, Charles Babbage propos o primeiro computador mecânico capaz de ler cartões perfurados e realizar cálculos matemáticos. Ele nunca foi construído devido a complexidade necessária e os elevados custos. Sua ideia serviu de base para que em 1842, Ada Lovelace escrevesse o primeiro algoritmo de computador, que poderia ser executado neste computador mecânico.

<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Babbages_Analytical_Engine%2C_1834-1871._%289660574685%29.jpg" alt="Computador mecânico de Babbage" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />
<br />

Ok, mas chega de história, falei tudo isso para dizer que nos cartões perfurados, tínhamos código binário de máquina. Eles eram lidos por esses dispositivos e interpretados por seus processadores. Em 1906, Herman Hollerith construiu a empresa que se tornaria a IBM depois. Isso é relevante, pois ele construiu computadores que liam cartões perfurados e executavam diferentes programas, dependendo do conteúdo dos cartões lidos. Isso permitia que o mesmo dispositivo fosse utilizado para realizar diferentes tarefas, sem a necessidade de reconstruir o dispositivo.

<img src="https://i.ytimg.com/vi/17On5ItcrBA/maxresdefault.jpg" alt="Máquina de Herman Hollerith" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />
<br />

Na década de 1940 e 1950, os computadores passaram a não ser apenas dispositivos mecânicos, mas sim dispositivos eletrônicos. Os cartões perfurados foram substituídos por fitas magnéticas, que além de conseguir guardar uma quantidade maior de dados, podiam ser manipuladas mais rapidamente. Começaram a surgir mnemônicos, que são palavras que representam as instruções de máquina, como ADD para adição, SUB para subtração, etc. Esses mnemônicos eram escritos em uma linguagem de montagem (**Assemly**), que é uma linguagem de baixo nível, mas mais fácil de ler e escrever do que o código de máquina. Os programas passavam por um montador (**Assembler**), que convertia os mnemônicos em código de máquina, para então gravar eles em fitas magnéticas.

<img src="https://miro.medium.com/v2/resize:fit:357/1*PardCSMthwItwS6i5CeWwQ.png" alt="Exemplo de código Assembly" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />
<br />

Mesmo com o Assembly ajudando o processo de desenvolvimento de programas, ele ainda demandava um conhecimento bastante profundo do hardware utilizado para sua execução. O maior problema é que os programadores precisavam deste conhecimento para escrever seus programas, o que tornava o processo de desenvolvimento muito complexo e demorado. Neste momento, para sanar está dor, surgem as linguagem de programação de alto nível, que se assemelham mais com a linguagem das pessoas, como o inglês. Elas permitiam que as pessoas pudessem escrever seus programas sem precisar conhecer os detalhes do hardware que seria utilizado para sua execução.

Os códigos gerados por essas linguagens de alto nível precisavam ser convertidos em código de máquina, para que os processadores pudessem executá-los. Para atender está demanda, são desenvolvidos programas especiais chamados de ***compiladores***. Eles tem como maior propósito ler o código escrito em uma linguagem e gerar o código de máquina correspondente. Existem diversos tipos e compiladores, cada um com suas características e funcionalidades. Dentre eles, existem um compilador que um merece atenção especial, o GCC ([*GNU Compiler Collection*](https://gcc.gnu.org/)).

:::tip[Como os programas são interpretados pelo computador]

<iframe width="560" height="315" src="https://www.youtube.com/embed/QXjU9qTsYCc?si=sJ8t1jfRnkC2t27h" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

Legal, chegamos ao ponto que temos como escrever nossos programas em uma linguagem de alto nível e compilar eles para o nosso processador. Mas ainda precisamos falar como vamos escrever nossos programas e como vamos compilar eles. Para isso, precisamos de um ambiente de desenvolvimento e o compilador para gerar o nosso código de máquina.

## 2. O compilador 

Pessoal, antes de iniciarmos o nosso estudo da linguagem C, vamos verificar qual o processo para transformar esse código em um programa executável pelo nosso computador. Vamos conseguir fazer isso utilizando algumas ferramentas. O nosso programa base será o seguinte:

```c
// Programa de HelloWorld em C
// ola.c
#include <stdio.h>
#include <stdlib.h>

int main() {
    printf("Ola mundo!\n");
    return 0;
}
```

Legal, temos nosso primeiro programa, que logo menos vamos avaliar o que está fazendo , mas primeiro vamos compilar ele. Cada sistema operacional possui um conjunto de compiladores que podem ser utilizados. Quem estiver utilizando o Windows, pode utilizar o  ***MinGW*** ([*Minimalist GNU for Windows*](https://www.mingw-w64.org/)). Ele pode ser instalado de diversas maneiras no sistema operacional, a mais simples é utilizando ele por meio de um ambiente de desenvolvimento que já o inclua, como o ***Code::Blocks*** ([*Code::Blocks*](http://www.codeblocks.org/)) ou o ***Dev-C++*** ([*Dev-C++*](https://www.bloodshed.net/)).

> "Pô Murilão, sério mesmo? Eu já uso o Visual Studio Code, não posso utilizar ele aqui também?"

Ooo caramba! Conhecer outras ferramentas é bom também! Não deixe de testar esses ambientes de desenvolvimento também! Mas vamos a pergunta, sim é possível utilizar o Visual Studio Code para compilar programas em C. Podemos utilizar a própria [documentação](https://code.visualstudio.com/docs/cpp/config-mingw) do Visual Studio Code para realizar essa configuração. Eu vou utilizar o WSL com o VIsual Studio Code. Aqui tem uma abordagem da documentação do [Visual Studio Code](https://code.visualstudio.com/docs/cpp/config-wsl).

:::tip[Instalando o WSL]

WSL significa *Windows Subsystem for Linux*, que é um subsistema do Windows que permite executar distribuições Linux diretamente no Windows. Ele é uma opção para quem deseja utilizar ferramentas e ambientes de desenvolvimento do Linux no Windows, sem precisar de uma máquina virtual ou dual boot.

Pessoal se você precisar de ajuda para instalar o WSL, recomendo a leitura do artigo: [*Como instalar o Linux no Windows com o WSL*](https://learn.microsoft.com/pt-br/windows/wsl/install).

:::

Vamos verificar se o WSL está com o GCC instalado. Para isso, abra o terminal do WSL e execute o seguinte comando:

```bash
gcc --version
```

Se o GCC estiver instalado, você verá a versão do compilador instalada. Caso contrário, você precisará instalá-lo. Para instalar o GCC no WSL, execute o seguinte comando:

```bash
sudo apt update && sudo apt install build-essential
```

:::danger[Instalação do GCC no WSL]

Aqui pessoal, estou considerando que você está utilizando uma distribuição baseada no Debian, como o Ubuntu. Se você estiver utilizando outra distribuição, o comando de instalação pode ser diferente. Consulte a documentação da sua distribuição para obter mais informações.

:::

Beleza, agora com o GCC instalador, vamos conseguir compilar nosso programa. Para isso, vou abrir o Visual Studio Code no diretório onde está o arquivo `ola.c`. Para isso, abra o terminal do WSL e execute o seguinte comando:

```bash
code ola.c
```
Isso abrirá o Visual Studio Code no diretório onde está o arquivo `ola.c`. Agora, vamos compilar o programa. No terminal do WSL, execute o seguinte comando:

```bash
gcc ola.c -o ola
```
 E agora para executar nosso programa, vamos utilizar o seguinte comando:

 ```bash
 ./ola
```

:::tip[Navegando para os diretórios do Windows no WSL]

Pessoal o WSL instala o Linux dentro do Windows, com diretórios separados. Mas calma! Ainda é possível acessar os diretórios do Windows a partir do WSL. Para isso, você pode navegar até o diretório `/mnt/c`, que é onde o WSL monta o disco C do Windows. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/51Ci4RUuEVs?si=72qOn4N1xMXvb6pE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::


:::tip[Compilando programas C no MacOS]

Pessoal, quem estiver utilizando o MacOS, é possível utilizar o compilador Clang, que já vem instalado por padrão no sistema operacional. Para verificar se o Clang está instalado, abra o terminal e execute o seguinte comando:

```bash
clang --version
```
Se o Clang estiver instalado, você verá a versão do compilador instalada. Caso contrário, você precisará instalá-lo. Você pode fazer isso instalando o XCode Command Line Tools, que pode ser instalado executando o seguinte comando no terminal:

```bash
xcode-select --install
```

Para compilar os programas, você pode utilizar o seguinte comando:

```bash
clang ola.c -o ola
```

:::

## 3. Referencias

Pessoal deixei aqui mais algumas referências que eu acredito que podem ser úteis para vocês:

<iframe width="560" height="315" src="https://www.youtube.com/embed/3pfRvy_gfqY?si=7yK01ZqhCWivgly6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/YShlJiUntic?si=SCQLPNy8lyTfQ8dR" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/afUiVvDUIRA?si=zh_y7dMU2vMbRLBB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SNyh-cubxaU?si=QMFYNIkN0GxKpKn1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/EFmxPMdBqmU?si=7Ry1bfAdNR7GDDh1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>