---
title: Sintaxe da Linguagem C
sidebar_position: 2
slug: /c-lang-sintax
---

Legal pessoal, conversamos sobre como é realizado o processo de compilação do nosso código e como um programa é convertido em um executável. Agora vamos dar uma olhada na sintaxe da linguagem C. Ela traz o conjunto de regras sobre como escrever código fonte em C. Vamos aproveitar e praticar com alguns exercícios sobre.

## 1. Sintaxe Básica do Ola Mundo

Pessoal para iniciar nosso estudo de C, vamos escrever nosso primeiro programa e avaliar ele:

```c
// ola.c
#include <stdio.h>
#include <stdlib.h>

int main() {
    printf("Ola mundo!\n");
    return 0;
}
```

:::tip[O programa "Hello World"]

O primeiro programa que a maior parte dos programadores escreve quando vai iniciar o estudo de uma ferramenta ou linguagem é o "Hello World" dela. Pode parecer simples, mas este programa tem por objetivo familiarizar o programador com o básico necessário para utilizar aquela ferramenta. Ela é um marco inicial no processo de aprendizado e um passo que traz uma resposta imediata quanto a seu funcionamento. Mais pode ser visto [aqui](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program).

:::

Beleza, vamos entender o que cada elemento do nosso código faz:

- `#include <stdio.h>`: Esta linha inclui a biblioteca padrão de entrada e saída do C, que nos permite usar funções como `printf` para imprimir texto na tela.
- `#include <stdlib.h>`: Esta linha inclui a biblioteca padrão de utilidades do C, que nos permite usar funções como `exit` e `malloc`. Nenhum deles foi utilizado neste exemplo, mas já vamos ver como utilizá-los.
- `int main()`: Esta linha define a função principal do programa, que é o ponto de entrada. Todo programa C deve ter uma função `main`. A sua execução começa por aqui.
- `{ ... }`: As chaves delimitam o início e o fim do corpo da função `main`. A linguagem C utiliza chaves para realizar agrupamentos de código, como funções, estruturas e blocos.
- `printf("Ola mundo!\n");`: Esta linha chama a função `printf` para imprimir o texto "Ola mundo!" na tela. O `\n` é um caractere de nova linha, que move o cursor para a linha seguinte. Vamos avaliar esse comando mais a fundo.
- `return 0;`: Esta linha indica que o programa terminou com sucesso. O valor `0` é retornado para o sistema operacional, indicando que não houve erros durante a execução.
- `// ola.c`: Este é o comentário de uma linha, que é ignorado pelo compilador. Comentários são usados para documentar o código e torná-lo mais legível. No C, comentários de uma linha começam com `//`, enquanto comentários de várias linhas são delimitados por `/*` e `*/`.

Legal, agora que avaliamos cada um dos elementos do nosso código, vamos compilar e executar ele. Para isso, no terminal, vamos utilizar o comando:

```bash
# Dentro do diretório onde está o arquivo ola.c
gcc ola.c -o ola
```

Vamos compreender um pouco mais sobre este processo. Primeiro é preciso compreender o que está acontecendo aqui. Não temos a execução do nosso programa, mas sim a compilação dele. O comando `gcc` é o compilador de C, que converte o código fonte em um executável. O parâmetro `-o ola` especifica o nome do arquivo executável que será gerado. Durante o processo de compilação, o compilador verifica a sintaxe do código, realiza a análise semântica e gera o código objeto. Este código objeto é vinculado com as bibliotecas necessárias para criar o executável final. Este processo é chamado de "linkagem". Após a sua finalização, o executável `ola` é criado no mesmo diretório.

:::note[O processo de compilação]

Pessoal existem algumas etapas que ocorrem durante o processo de compilação. Primeiro podemos criar nossos arquivos traduzidos para o assembler, informando para o compilador que desejamos gerar esse código:

```bash
gcc -S ola.c
```

Isso vai gerar um arquivo `ola.s` que contém o código em assembler. O assembler é uma linguagem de baixo nível que é mais próxima do código de máquina, mas ainda legível por humanos. Em seguida, podemos compilar esse código assembler para gerar o código objeto:

```bash
gcc -c ola.c
```
Isso vai gerar um arquivo `ola.o` que contém o código objeto. O código objeto é uma representação binária do código que ainda não está completamente vinculado. Por fim, podemos vincular o código objeto com as bibliotecas necessárias para criar o executável:

```bash
gcc ola.o -o ola
```

Isso vai gerar o executável `ola`. O processo de compilação pode ser dividido em três etapas: pré-processamento, compilação e linkagem. O pré-processamento inclui a inclusão de bibliotecas e a expansão de macros. A compilação converte o código fonte em código objeto, e a linkagem combina o código objeto com as bibliotecas necessárias para criar o executável final.

<iframe width="560" height="315" src="https://www.youtube.com/embed/N2y6csonII4?si=RCpBQLlvbE8TVmnu" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

Beleza, agora para executar o programa, basta rodar o comando:

```bash
./ola
```

Se verificarmos no terminal, o arquivo `ola` é um arquivo executável. Podemos verificar isso com o comando `file`:

```bash
file ola
```

:::tip[ELF - Executable and Linkable Format]

<iframe width="560" height="315" src="https://www.youtube.com/embed/Ia5jyz8sOCM?si=1xbBUWskrjawQikx" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

Legal, agora vamos avançar um pouco com a sintaxe do C.

## 2. Sintaxe Básica do C

Já vimos alguns pontos importantes da sintaxe do C:
- Todo programa em C deve possuir uma função `main`, que é o ponto de entrada do programa;
- A linguagem C é compilada, ou seja, o código fonte é convertido em um executável antes de ser executado;
- O C utiliza chaves `{}` para delimitar blocos de código, como funções e estruturas.

Agora vamos para mais alguns detalhes importantes, vamos analisar o nosso segundo programa de exemplo:

```c
// 01_programa_base.c

#include <stdio.h>

int main(){
        int valor_a;
        int valor_b, valorC = 10;
        printf("O valor das variaveis: %i, %d, %i\n", valor_a, valor_b, valorC);
        valor_a = 10;
        valor_b = valor_a*2 + valorC;
        printf("O valor das variaveis: %i, %d, %i\n", valor_a, valor_b, valorC);
        return 0;
}  

```

Vamos compilar e executar este programa. O que mais interessa neste momento é a sintaxe do C e alguns conceitos que vamos analisar aqui.

```bash
gcc 01_programa_base.c -o 01_programa_base
./01_programa_base
```

A saída do programa deverá ser algo parecido com:

```bash
O valor das variaveis: -47394720, 21870, 10
O valor das variaveis: 10, 30, 10
```

> "Opa opa Murilão! A segunda linha está igual, mas a primeira está com valores diferentes, o que está acontecendo?"

Boa gente, vamos avaliar isso. C é uma linguagem estática, ou seja, as variáveis devem ser declaradas antes de serem utilizadas. No nosso exemplo, as variáveis `valor_a` e `valor_b` são declaradas, mas não inicializadas antes de serem utilizadas na primeira chamada do `printf`. Isso significa que elas contêm valores aleatórios da memória, o que resulta em uma saída inesperada.

Outro ponto importante de se observar, que as variáveis são posições de memória que nós utilizamos para armazenar valores. No C, as variáveis devem ser declaradas com um tipo específico, como `int`, `float`, `char`, etc. No nosso exemplo, `valor_a` e `valor_b` são declaradas como inteiros (`int`), enquanto `valorC` é inicializada com o valor `10`. Os tipos que chamamos de primitivos são os tipos básicos da linguagem, como `int`, `float`, `char`, etc. Eles são usados para armazenar valores simples, como números inteiros, números de ponto flutuante e caracteres.


| Tipo                 | Descrição                                      | Exemplo de declaração                           | Tamanho (bytes) |
| -------------------- | ---------------------------------------------- | ----------------------------------------------- | --------------- |
| `_Bool`              | Valor booleano (0 ou 1), veio no C99. Incluir com \<stdbool.h\>                      | `_Bool flag = 1;`                               | 1               |
| `char`               | Caractere (geralmente ASCII)                   | `char c = 'A';`                                 | 1               |
| `signed char`        | Caractere com sinal, alcance típico −128 a 127 | `signed char sc = -10;`                         | 1               |
| `unsigned char`      | Caractere sem sinal, alcance 0 a 255           | `unsigned char uc = 200;`                       | 1               |
| `short`              | Inteiro curto com sinal                        | `short s = 1000;`                               | 2               |
| `unsigned short`     | Inteiro curto sem sinal                        | `unsigned short us = 60000;`                    | 2               |
| `int`                | Inteiro padrão com sinal                       | `int i = 12345;`                                | 4               |
| `unsigned int`       | Inteiro padrão sem sinal                       | `unsigned int ui = 3000000000U;`                | 4               |
| `long`               | Inteiro longo com sinal                        | `long l = 1234567890L;`                         | 8               |
| `unsigned long`      | Inteiro longo sem sinal                        | `unsigned long ul = 4000000000UL;`              | 8               |
| `long long`          | Inteiro muito longo com sinal                  | `long long ll = 1234567890123LL;`               | 8               |
| `unsigned long long` | Inteiro muito longo sem sinal                  | `unsigned long long ull = 1000000000000000ULL;` | 8               |
| `float`              | Ponto flutuante simples precision              | `float f = 3.14f;`                              | 4               |
| `double`             | Ponto flutuante dupla precision                | `double d = 3.1415926535;`                      | 8               |
| `long double`        | Ponto flutuante estendido                      | `long double ld = 3.141592653589793L;`          | 16              |

Legal, agora temos os tipos das nossas variáveis vamos ver um pouco mais sobre o nosso programa. Vamos aproveitar para falar dos nomes das variáveis. No C, os nomes das variáveis devem seguir algumas regras:
- Devem começar com uma letra (a-z, A-Z) ou um sublinhado (_);
- Podem conter letras, números (0-9) e sublinhados;
- Não podem conter espaços ou caracteres especiais (como @, #, $, etc.);
- Não podem ser palavras reservadas da linguagem (como `int`, `return`, `if`, etc.);
- São sensíveis a maiúsculas e minúsculas (por exemplo, `valor_a` e `Valor_A` são considerados diferentes).

Dos tópicos anteriores, acho que a mais interessante para analisar é a questão de palavras reservadas. Elas são reservadas pois são utilizadas pela linguagem para definir estruturas e comandos. Por exemplo, `int` é uma palavra reservada que define um tipo de dado inteiro, `return` é usada para retornar um valor de uma função, e `if` é usada para criar uma estrutura condicional. Não podemos utilizar essas palavras como nomes de variáveis, pois isso causaria conflitos e erros de compilação.

| Palavra-reservada | Categoria                      |
| ----------------- | ------------------------------ |
| auto              | Storage-class                  |
| register          | Storage-class                  |
| static            | Storage-class                  |
| extern            | Storage-class                  |
| typedef           | Storage-class                  |
| \_Thread\_local   | Storage-class (C11)            |
| \_Atomic          | Qualificador/Atomicidade (C11) |
| const             | Qualificador                   |
| volatile          | Qualificador                   |
| restrict          | Qualificador (C99)             |
| void              | Tipo                           |
| char              | Tipo                           |
| short             | Tipo                           |
| int               | Tipo                           |
| long              | Tipo                           |
| float             | Tipo                           |
| double            | Tipo                           |
| signed            | Tipo (qualificador)            |
| unsigned          | Tipo (qualificador)            |
| \_Bool            | Tipo (C99)                     |
| \_Complex         | Tipo (C99)                     |
| \_Imaginary       | Tipo (C99)                     |
| \_Alignas         | Align-spec (C11)               |
| \_Alignof         | Align-spec (C11)               |
| \_Noreturn        | Função (C11)                   |
| \_Static\_assert  | Asserção (C11)                 |
| if                | Controle condicional           |
| else              | Controle condicional           |
| switch            | Controle condicional           |
| case              | Controle condicional           |
| default           | Controle condicional           |
| for               | Laço                           |
| while             | Laço                           |
| do                | Laço                           |
| break             | Desvio                         |
| continue          | Desvio                         |
| goto              | Desvio                         |
| return            | Desvio                         |
| sizeof            | Operador                       |
| inline            | Especificador de função (C99)  |
| enum              | Construção de tipo             |
| struct            | Construção de tipo             |
| union             | Construção de tipo             |

Legal agora também temos nossas palavras reservadas! Vamos ver um pouco mais ainda sobre este programa. As instruções em C são terminadas por ponto e vírgula (`;`). Isso indica o final de uma instrução. No nosso exemplo, cada linha dentro da função `main` termina com um ponto e vírgula, exceto as linhas que contêm chaves `{}` que delimitam blocos de código. Outro ponto interessante para observar é o que significa C ser uma linguagem de tipagem estática. Isso significa que os tipos das variáveis são verificados em tempo de compilação, e não em tempo de execução. Ou seja, o compilador verifica se as variáveis estão sendo usadas corretamente de acordo com seus tipos antes de gerar o executável. Isso ajuda a evitar erros comuns, como tentar realizar operações inválidas entre tipos diferentes.

Outro ponto interessante para observar aqui, o operador de atribuição `=` é utilizado para atribuir valores às variáveis. No nosso exemplo, `valor_a` é atribuído o valor `10`, e `valor_b` é atribuído o resultado da expressão `valor_a * 2 + valorC`. O C também possui operadores aritméticos, como `+`, `-`, `*`, `/` e `%`, que são usados para realizar operações matemáticas. Mais sobre isso logo menos.

Agora vamos para nossa função de exibição, o `printf()`. Ela é uma função da biblioteca padrão do C que permite imprimir texto formatado na saída padrão (em geral, o console). Ela recebe como primeiro argumento uma string de formato, que diz como o texto deve ser exibido, e os argumentos seguintes são os valores a serem exibidos. No nosso exemplo, a string de formato é `"O valor das variaveis: %i, %d, %i\n"`, onde `%i` e `%d` são especificadores de formato que indicam que os valores correspondentes devem ser exibidos como inteiros. O `\n` é um caractere de nova linha, que move o cursor para a linha seguinte.

| Especificador | Significado                                                        | Exemplo de uso                                               |
| ------------- | ------------------------------------------------------------------ | ------------------------------------------------------------ |
| `%d` / `%i`   | inteiro decimal com sinal                                          | `int i = -42; printf("%i\n", i);`                        |
| `%u`          | inteiro decimal sem sinal                                          | `unsigned u = 42U; printf("%u\n", u);`                   |
| `%o`          | inteiro em octal sem sinal                                         | `unsigned u = 10; printf("%o\n", u);`                    |
| `%x` / `%X`   | inteiro em hexadecimal (minúsculo/maiúsculo)                       | `unsigned u = 255; printf("%X\n", u);`                   |
| `%f` / `%F`   | ponto flutuante (notação decimal)                                  | `double d = 3.14; printf("%F\n", d);`                    |
| `%e` / `%E`   | ponto flutuante em notação científica                              | `double d = 0.00123; printf("%e\n", d);`                 |
| `%g` / `%G`   | formato automático (`%f` ou `%e`, o que for menor)                 | `double d = 123456.0; printf("%g\n", d);`                |
| `%a` / `%A`   | ponto flutuante em notação hexadecimal                             | `double d = 10.5; printf("%a\n", d);`                    |
| `%c`          | caractere                                                          | `char c = 'Z'; printf("%c\n", c);`                       |
| `%s`          | string (cadeia de `char`)                                          | `char *s = "Olá"; printf("%s\n", s);`                    |
| `%p`          | endereço de ponteiro                                               | `int x; printf("%p\n", (void*)&x);`                      |
| `%n`          | escreve em um inteiro o número de caracteres já impressos até aqui | `int count; printf("abc%n\n", &count); /* count == 3 */` |
| `%%`          | imprime o literal `%`                                              | `printf("100%% concluído\n");`                            |

Legal, temos só mais um detalhes que são os caracteres de escape. Eles são utilizados para representar caracteres especiais dentro de strings. No nosso exemplo, usamos `\n` para representar uma nova linha. Outros caracteres de escape comuns incluem:

| Sequência | Descrição                                         | Exemplo de uso                               |
| --------- | ------------------------------------------------- | -------------------------------------------- |
| `\n`      | Nova linha (LF)                                   | `printf("Linha1\nLinha2\n");`                |
| `\t`      | Tabulação horizontal                              | `printf("Col1\tCol2\n");`                    |
| `\r`      | Retorno de carro (CR)                             | `printf("12345\rAB\n"); /* imprime AB345 */` |
| `\a`      | Alerta (beep)                                     | `printf("Atenção!\a\n");`                    |
| `\b`      | Backspace                                         | `printf("ABC\bD\n"); /* imprime ABD */`      |
| `\f`      | Form feed (avança para nova “página”)             | `printf("Página1\fPágina2\n");`              |
| `\v`      | Tabulação vertical                                | `printf("Linha1\vLinha2\n");`                |
| `\\`      | Barra invertida (`\`)                             | `printf("C:\\Windows\\System32\n");`         |
| `\'`      | Aspas simples (`'`)                               | `printf("It\'s OK\n");`                      |
| `\"`      | Aspas duplas (`"`)                                | `printf("Ela disse: \"%s\"\n", "Olá");`      |
| `\?`      | Ponto de interrogação                             | `printf("E se eu disser\?\n");`              |
| `\nnn`    | Caractere pelo código octal (até 3 dígitos)       | `printf("\101\n"); /* ’A’ */`                |
| `\xhh`    | Caractere pelo código hexadecimal (até 2 dígitos) | `printf("\x41\n"); /* ’A’ */`                |

Beleza! Agora vamos avançar um pouco mais.

## 3. Trabalhando com Variáveis

Aqui vamos escrever um programa que permite o usuário inserir dois números inteiros e vamos exibir a soma deles.

```c
// 02_soma.c
#include <stdio.h>
 int main(){
    int val1, val2, res;
    printf("Informe dois valores:\n");
    scanf("%d", &val1);
    scanf("%d", &val2);
    res = val1 + val2;
    printf("Resultado da soma: %d\n", res);
    return 0;
}
```

Aqui temos algumas novidades a tratar! Primeiro vamos da mais simples, a soma dos valores. O operador `+` faz parte dos operadores aritméticos do C, que são usados para realizar operações matemáticas. Outros operadores aritméticos incluem `-` (subtração), `*` (multiplicação), `/` (divisão) e `%` (módulo). No nosso exemplo, usamos o operador `+` para somar os valores de `val1` e `val2`, e armazenamos o resultado na variável `res`.

| Operador | Descrição                                    | Exemplo          |
| -------- | -------------------------------------------- | ---------------- |
| `+`      | Adição                                       | `c = a + b;`     |
| `-`      | Subtração                                    | `c = a - b;`     |
| `*`      | Multiplicação                                | `c = a * b;`     |
| `/`      | Divisão inteira (ou em ponto-flutuante)      | `c = a / b;`     |
| `%`      | Módulo (resto da divisão inteira)            | `c = a % b;`     |
| `++`     | Incremento (pré ou pós)                      | `++a;` ou `a++;` |
| `--`     | Decremento (pré ou pós)                      | `--a;` ou `a--;` |
| `+=`     | Adição e atribuição (`a = a + valor`)        | `a += 5;`        |
| `-=`     | Subtração e atribuição (`a = a - valor`)     | `a -= 2;`        |
| `*=`     | Multiplicação e atribuição (`a = a * valor`) | `a *= 3;`        |
| `/=`     | Divisão e atribuição (`a = a / valor`)       | `a /= 4;`        |
| `%=`     | Módulo e atribuição (`a = a % valor`)        | `a %= 6;`        |

Legal, agora vamos falar sobre a nossa entrada de dados do usuário, a função `scanf()`. Ela é usada para ler dados da entrada padrão (no nosso caso o teclado) e armazenar o resultado lido em um endereço de memória.

> "Murilão, calma lá! Você falou errado! Era para dizer que ela lê dados de entrada e guarda o resultado em uma variável."

Então, sim isso está correto. Mas tem um detalhe importante, nós precisamos que a função `scanf()` consiga modificar um dos parâmetros que passamos para ela. Isso traz um comportamento bastante interessante do C, a passagem por valor e por referência. Os parâmetros são passados para as funções por valor, ou seja, uma cópia do valor é passada para a função. No entanto, quando passamos o endereço de memória de uma variável (usando o operador `&`), estamos passando uma referência para a variável original. Isso permite que a função modifique o valor da variável original.

:::tip[Passagem por valor e por referência]

<iframe width="560" height="315" src="https://www.youtube.com/embed/KD8zanR034A?si=uujMMQ7I7G3yvN1o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

Os tipos de dados que utilizamos como texto formatador no `scanf()` são:

| Forma de leitura   | Tipo de dado lido  | Exemplo                      | Descrição                                                                    |
| ------------------ | ------------------ | ---------------------------- | ---------------------------------------------------------------------------- |
| `%d`               | `int`              | `scanf("%d", &i);`           | Lê inteiro decimal com sinal.                                                |
| `%i`               | `int`              | `scanf("%i", &i);`           | Lê inteiro em base automática (0x → hex, 0 → octal, senão decimal).          |
| `%u`               | `unsigned int`     | `scanf("%u", &u);`           | Lê inteiro decimal sem sinal.                                                |
| `%o`               | `unsigned int`     | `scanf("%o", &u);`           | Lê inteiro em base octal.                                                    |
| `%x` / `%X`        | `unsigned int`     | `scanf("%x", &u);`           | Lê inteiro em base hexadecimal.                                              |
| `%f`               | `float`            | `scanf("%f", &f);`           | Lê ponto flutuante (simples precisão).                                       |
| `%lf`              | `double`           | `scanf("%lf", &d);`          | Lê ponto flutuante dupla precisão.                                           |
| `%e` / `%E`        | `float` / `double` | `scanf("%e", &f);`           | Lê em notação científica (`1.23e+02`).                                       |
| `%c`               | `char`             | `scanf(" %c", &c);`          | Lê um caractere; o espaço antes do `%c` faz `scanf` pular whitespace.        |
| `%s`               | `char[]` (string)  | `scanf("%s", str);`          | Lê até o primeiro whitespace (não protege contra overflow).                  |
| `%[^\n]`           | `char[]` (scanset) | `scanf("%[^\n]", line);`     | Lê tudo até encontrar `\n` (newline).                                        |
| `%p`               | `void*`            | `scanf("%p", &ptr);`         | Lê um valor de ponteiro (endereço).                                          |
| `%n`               | `int*`             | `scanf("%d%n", &i, &count);` | Armazena em `count` o nº de caracteres consumidos até aqui.                  |
| `%*d`              | descarta (`int`)   | `scanf("%*d %d", &i);`       | O `*` suprime a atribuição: o primeiro inteiro é lido, mas não armazenado.   |
| `%5d`, `%10s` etc. | diversos           | `scanf("%5s", str);`         | O número entre `%` e o especificador limita o nº máximo de caracteres lidos. |

Legal, agora vamos falar sobre o operador de endereço `&`. Ele é usado para obter o endereço de memória de uma variável. No nosso exemplo, usamos `&val1` e `&val2` para passar o endereço de memória das variáveis `val1` e `val2` para a função `scanf()`. Isso permite que a função modifique o valor dessas variáveis diretamente na memória. Vamos trabalhar mais com este operador logo menos.

## 4. Estruturas de Decisão

As estruturas de controle são utilizadas para controlar o fluxo da execução de um programa. Elas permitem que o programa tome decisões para seguir diferentes fluxos de execução dado o estado atual do programa. A linguagem C possui algumas estruturas de decisão, vamos avaliar elas aqui.

```c
// 03_estrutura_decisao.c
#include <stdio.h>
int main(){
    int valor;
    printf("Informe um valor: ");
    scanf("%d", &valor);

    if (valor > 0) {
        printf("O valor é positivo.\n");
    } else if (valor < 0) {
        printf("O valor é negativo.\n");
    } else {
        printf("O valor é zero.\n");
    }

    return 0;
}
```

Esse programa é bastante simples e bastante direto para sua utilização, depois de compilar e executar o programa, ele vai solicitar para o usuário informar um valor. Esse valor é armazenado na variável `valor`, que é um inteiro. Aqui vem a utilização das estruturas de decisão. A estrutura `if` verifica primeiro se o valor é maior que zero. Em caso afirmativo, o programa imprime "O valor é positivo." na tela. Se não for, ele verifica se o valor é menor que zero. Se for, o programa imprime "O valor é negativo.". Se nenhuma das condições anteriores for verdadeira, significa que o valor é zero, e o programa imprime "O valor é zero.". 

Aqui cabe destacar o seguinte comportamento, apenas uma das condições será executada. Isso ocorre porque as estruturas de decisão são avaliadas sequencialmente. Assim que uma condição é verdadeira, o bloco de código correspondente é executado e o restante das condições é ignorado. É importante conhecer a forma como as estruturas de decisão são avaliadas para conseguir utilizá-las da melhor forma possível.

Outro detalhe bastante importante: em C, não existe o conceito de "verdadeiro" e "falso" como em outras linguagens. Em vez disso, qualquer valor diferente de zero é considerado verdadeiro, enquanto zero é considerado falso. Isso significa que podemos usar expressões aritméticas diretamente nas condições das estruturas de decisão. Mas atenção, o ponto que é verdade é que o valor zero é falso, todo o restante é considerado verdadeiro. 

Os operadores lógicos também são utilizados para combinar condições. Os operadores lógicos mais comuns são:

| Operador | Descrição        | Exemplo                      |
| -------- | ---------------- | ---------------------------- |
| `<`      | Menor que        | `if (a < b) printf("sim");`  |
| `>`      | Maior que        | `if (a > b) printf("sim");`  |
| `<=`     | Menor ou igual a | `if (a <= b) printf("sim");` |
| `>=`     | Maior ou igual a | `if (a >= b) printf("sim");` |
| `==`     | Igual a          | `if (a == b) printf("sim");` |
| `!=`     | Diferente de     | `if (a != b) printf("sim");` |


:::tip[Operador Ternário]

O operador ternário é uma forma concisa de escrever uma estrutura condicional simples. Ele tem a seguinte sintaxe:

```c
condição ? expressão_se_verdadeira : expressão_se_falsa;
```

Importante ficar claro que ele pode ser encadeado, mas utilizar esse recurso com cuidado, para não tornar o código mais difício de ler. Outro ponto importante para observar é que o operador ternário deve retornar um valor, ou seja, ele não deve ser usado para executar blocos de código como as estruturas `if` e `else`.

:::


Vamos ver um exemplo agora com mais uma estrutura de decisão, a `switch`. Ela é utilizada para avaliar uma expressão e executar um bloco de código correspondente ao valor da expressão. Vamos ver um exemplo:

```c
// 04_estrutura_switch.c
#include <stdio.h>

int main() {
    int dia;
    printf("Informe um número de 1 a 7 para o dia da semana: ");
    scanf("%d", &dia);

    switch (dia) {
        case 1:
            printf("Domingo\n");
            break;
        case 2:
            printf("Segunda-feira\n");
            break;
        case 3:
            printf("Terça-feira\n");
            break;
        case 4:
            printf("Quarta-feira\n");
            break;
        case 5:
            printf("Quinta-feira\n");
            break;
        case 6:
            printf("Sexta-feira\n");
            break;
        case 7:
        case 0: // Adicionando o caso 0 para o sábado também
            printf("Sábado\n");
            break;
        default:
            printf("Número inválido! Informe um número de 1 a 7.\n");
    }

    return 0;
}
```

Pessoal aqui o ponto principal para se observar é a estrutura `switch`. Ela avalia a variável `dia` e executa o bloco de código correspondente ao valor dessa variável. Cada `case` representa um valor possível para a variável, e o bloco de código correspondente é executado se a variável tiver aquele valor. O `break` é usado para sair do `switch` após a execução do bloco de código correspondente. Se não houver um `break`, o programa continuará executando os blocos de código dos próximos `case`, até que ele encontre um `break` ou o final do `switch`, como é o caso do valor `7` e do valor `0` no nosso exemplo. O `default` é usado para tratar casos em que a variável não corresponde a nenhum dos valores especificados nos `case`. Ele é opcional, mas é uma boa prática incluí-lo para lidar com entradas inválidas.

## 5. Estruturas de Repetição

As estruturas de repetição são utilizadas para executar um bloco de código várias vezes, enquanto uma condição for verdadeira. Elas são úteis quando precisamos repetir uma ação várias vezes, como percorrer elementos de um array ou realizar cálculos iterativos. A linguagem C possui três estruturas de repetição principais: `for`, `while` e `do-while`. Vamos ver cada uma delas.

```c
// 05_estrutura_for.c

#include <stdio.h>
int main() {
    int i;
    printf("Contagem de 1 a 10:\n");
    for (i = 1; i <= 10; i++) {
        printf("%d ", i);
    }
    printf("\n");
    return 0;
}
```

Legal, aqui temos um exemplo de utilização da estrutura `for`. Ela composta por 3 partes principais:
- Inicialização: `i = 1` é executada uma vez antes do início do loop. É onde definimos a variável de controle do loop.
- Condição: `i <= 10` é verificada antes de cada iteração do loop. Se for verdadeira, o bloco de código dentro do loop é executado. Se for falsa, o loop termina.
- Incremento: `i++` é executado após cada iteração do loop. É onde atualizamos a variável de controle do loop.

Em geral, essa estrutura é utilizada quando sabemos o número de iterações que queremos realizar. No nosso exemplo, estamos contando de 1 a 10, então sabemos que o loop deve ser executado 10 vezes.

Agora vamos ver um exemplo com a estrutura `while`.

```c
// 06_estrutura_while.c
#include <stdio.h>

int main() {
    int i = 1;
    printf("Contagem de 1 a 10:\n");
    while (i <= 10) {
        printf("%d ", i);
        i++;
    }
    printf("\n");
    return 0;
}
```

Aqui pessoal, o nosso exemplo é semelhante ao anterior, mas utilizando a estrutura `while`. Aqui a diferença é que a estrutura tem o funcionamento de repetir sua execução, enquanto a condição de teste for verdadeira. No nosso exemplo, a variável `i` é inicializada com o valor `1`, e o loop continua enquanto `i` for menor ou igual a `10`. Dentro do loop, imprimimos o valor de `i` e incrementamos `i` em `1`. Assim como no exemplo anterior, o loop será executado 10 vezes. Aqui uma observação importante, a variável de controle do loop pode ser alterada durante a sua execução, ele apenas será avaliada novamente quando o loop for executado novamente. Isso significa que se a condição de teste não for alterada, o loop pode se tornar infinito, ou seja, ele nunca vai terminar. Por isso é importante garantir que a condição de teste seja alterada dentro do loop, para evitar loops infinitos.

A estrutura `while` tem uma característica interessante, ela pode ter seu bloco de código nunca executado. Isso acontece quando a condição de teste já é falsa antes do loop ser executado. Vamos ver um exemplo disso:

```c
// 07_estrutura_while_nunca_executado.c
#include <stdio.h>

int main() {
    int i = 11; // Inicializando i com um valor maior que 10
    printf("Contagem de 1 a 10:\n");
    while (i <= 10) {
        printf("%d ", i); // Este bloco nunca será executado
        i++;
    }
    printf("\n");
    return 0;
}
```

Aqui no momento que a condição de teste é avaliada, ela já é falsa, então o bloco de código dentro do loop nunca será executado. Isso é importante para se ter em mente, pois pode levar a comportamentos inesperados se não for tratado corretamente. Agora, vamos alterar esse programa para já verificarmos o funcionamento da estrutura `do-while`.

```c
// 08_estrutura_do_while.c
#include <stdio.h>

int main() {
    int i = 11; // Inicializando i com um valor maior que 10
    printf("Contagem de 1 a 10:\n");
    do {
        printf("%d ", i); // Este bloco será executado pelo menos uma vez
        i++;
    } while (i <= 10);
    printf("\n");
    return 0;
}
```

Repare que aqui temos quase o mesmo código do exemplo anterior, mas agora estamos utilizando a estrutura `do-while`. A diferença é que o bloco de código dentro do `do` será executado pelo menos uma vez, mesmo que a condição de teste seja falsa. Isso significa que, mesmo que `i` seja inicializado com um valor maior que `10`, o programa ainda imprimirá o valor de `i` uma vez antes de verificar a condição de teste.

:::danger[Uma palavra sobre o Goto]

O `goto` em C desempenha um papel histórico e pragmático: ele oferece um salto incondicional para outra parte do código, o que em certas situações—como em rotinas de tratamento de erro ou em máquinas de estados muito simples—pode simplificar a lógica de limpeza de recursos (por exemplo, liberar memória ou fechar arquivos antes de sair de várias camadas de funções). Em programas de baixo nível, onde cada ciclo e cada instrução importam, o `goto` chega a ser útil para gerar código mais eficiente, evitando empilhamentos profundos de chamadas de função ou a repetição de blocos de limpeza em vários pontos de saída.

No entanto, o uso indiscriminado de `goto` costuma gerar “código espaguete”: saltos espalhados tornam difícil entender o fluxo de execução, complicam a manutenção e aumentam a probabilidade de erros (como pular acidentalmente inicializações ou qualificações de variáveis). Por isso, a recomendação geral da comunidade é privilegiar construções de linguagem estruturadas—`if/else`, `for`, `while`, `switch`—e, para tratamento de erro, adotar padrões como código de retorno e blocos `cleanup` centralizados, evitando saltos arbitrários e preservando a clareza e robustez do software.

<iframe width="560" height="315" src="https://www.youtube.com/embed/AKJhThyTmQw?si=rCrdfpBqxDgHnG6M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

<iframe width="560" height="315" src="https://www.youtube.com/embed/8bmEhtMVrhk?si=8w1g3NUJZWESi8eV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />
:::

## 6. Funções

Legal, até aqui falamos de programas bastante pequenos. Eles tem por objetivo nos auxiliar a compreender como a linguagem C funciona. Por que compreender isso é importante? Porque agora vamos ver um conceito que auxilia demais durante o desenvolvimento de programas mais complexos, ou ainda quando desejamos deixar nosso código mais modular e simples de se utilizar, as funções.

De novo, ainda vamos continuar vendo programas pequenos, mas meu objetivo ao apresentar o conceito das funções é deixar claro para vocês que elas nos trazem bastante flexibilidade e organização no código. Vamos ver o exemplo de um programa que realiza as quatro operações matemáticas básicas (adição, subtração, multiplicação e divisão) utilizando funções.

```c
// 09_funcoes.c
#include <stdio.h>
// Função para somar dois números
int somar(int a, int b) {
    return a + b;
}
// Função para subtrair dois números
int subtrair(int a, int b) {
    return a - b;
}
// Função para multiplicar dois números
int multiplicar(int a, int b) {
    return a * b;
}
// Função para dividir dois números
double dividir(int a, int b) {
    if (b == 0) {
        printf("Erro: Divisão por zero!\n");
        return 0; // Retorna 0 em caso de divisão por zero
    }
    return (double)a / b;
}

int main() {
    int num1, num2;
    printf("Informe dois números inteiros:\n");
    scanf("%d %d", &num1, &num2);

    printf("Soma: %d\n", somar(num1, num2));
    printf("Subtração: %d\n", subtrair(num1, num2));
    printf("Multiplicação: %d\n", multiplicar(num1, num2));
    printf("Divisão: %.2f\n", dividir(num1, num2));

    return 0;
}
```

Aqui tem bastante coisa acontecendo! Fiquem comigo para que possamos estudar essa sintaxe em conjunto! Vamos lá!

Primeiro vamos compreender como é a estrutura de uma função em C. Ela possui um anatomia própria, que é composta por:

- Tipo de retorno: o tipo de dado que a função irá retornar. No nosso exemplo, as funções `somar`, `subtrair` e `multiplicar` retornam um `int`, enquanto a função `dividir` retorna um `double`.
- Nome da função: o nome que será utilizado para chamar a função. No nosso exemplo, as funções são chamadas `somar`, `subtrair`, `multiplicar` e `dividir`.
- Parâmetros: os valores que serão passados para a função. No nosso exemplo, as funções recebem dois parâmetros do tipo `int`, exceto a função `dividir`, que recebe dois parâmetros do tipo `int` e retorna um `double`.
- Corpo da função: o bloco de código que será executado quando a função for chamada. No nosso exemplo, cada função possui um corpo que realiza a operação matemática correspondente e retorna o resultado.

Aqui tem um ponto importante para se observar, as funções possuem uma forma específica de serem caracterizadas. Essa forma é chamada de assinatura da função. Analisando as assinaturas das funções que o compilador sabe que elas são diferentes, mesmo que os nomes sejam iguais. A assinatura de uma função é composta pelo nome da função, seu tipo de retorno e pelos tipos dos parâmetros. 

As funções em C precisão ser declaradas antes de serem utilizadas. Isso significa que o compilador precisa conhecer a assinatura da função antes de encontrá-la no código. No nosso exemplo, as funções são declaradas antes da função `main`, o que permite que elas sejam chamadas dentro da função `main`. Também é possível declarar as funções após a função `main`, mas nesse caso precisamos utilizar uma declaração prévia da função, que é uma forma de informar ao compilador sobre a assinatura da função antes de sua definição. A declaração prévia é feita da seguinte forma:

```c
// Declaração prévia da função
int somar(int a, int b);
```

> "Mas Murilão não é só declarar a função antes da `main` que já está tudo certo?"	

Quando estamos trabalhando com apenas um arquivo fonte, é possível fazer isso. Mas quando trabalhamos com múltiplos arquivos fonte ou ainda quando estamos trabalhando com bibliotecas, é necessário utilizar a declaração prévia para informar ao compilador sobre a assinatura da função antes de sua definição. Isso é especialmente importante quando estamos trabalhando com cabeçalhos (`.h`) e arquivos de implementação (`.c`).

Outro ponto importante é que as funções podem ser chamadas dentro de outras funções. No nosso exemplo, a função `main` chama as funções `somar`, `subtrair`, `multiplicar` e `dividir` para realizar as operações matemáticas. Isso permite que o código seja modularizado e organizado, facilitando a manutenção e a leitura do código. Quando vamos utilizar uma função, é importante passar os parâmetros corretos para ela. No nosso exemplo, as funções recebem dois parâmetros do tipo `int`, que são os números que serão utilizados nas operações matemáticas. Quando chamamos a função, passamos os valores das variáveis `num1` e `num2` como argumentos.

Podemos sobrecarregar funções em C, ou seja, podemos ter várias funções com o mesmo nome, mas com assinaturas diferentes. Vamos ver um exemplo disso:

```c
// 09_funcoes_overload.c
#include <stdio.h>
// Função para somar dois inteiros
int somar(int a, int b) {
    return a + b;
}
// Função para somar dois números de ponto flutuante
double somar(double a, double b) {
    return a + b;
}
// Função para somar três inteiros
int somar(int a, int b, int c) {
    return a + b + c;
}
int main() {
    int num1 = 5, num2 = 10, num3 = 15;
    double num4 = 2.5, num5 = 3.5;

    printf("Soma de dois inteiros: %d\n", somar(num1, num2));
    printf("Soma de dois números de ponto flutuante: %.2f\n", somar(num4, num5));
    printf("Soma de três inteiros: %d\n", somar(num1, num2, num3));

    return 0;
}
```

Aqui temos um exemplo de sobrecarga de funções. Temos três funções chamadas `somar`, mas cada uma tem uma assinatura diferente. A primeira função recebe dois parâmetros do tipo `int`, a segunda recebe dois parâmetros do tipo `double` e a terceira recebe três parâmetros do tipo `int`. Quando chamamos a função `somar`, o compilador escolhe a função correta com base nos tipos dos argumentos passados. Isso permite que possamos utilizar o mesmo nome de função para realizar operações diferentes, dependendo dos tipos dos parâmetros.

Vamos avançar mais com o uso de funções assim que avançarmos um pouco mais com a sintaxe do C.

## 7. Arrays

Legal, agora temos vários elementos base para construir nossos programas. Vamos analisar agora alguns outros elementos que vão permitir que nossos programas implementem alguns outros comportamentos mais complexos. Primeiro vamos analisar os arrays. Eles são utilizados como uma forma de armazenar diferentes valores do mesmo tipo na memória de forma contígua. Isso significa que os valores são armazenados em posições de memória adjacentes, o que permite acessar os valores de forma rápida e eficiente. Vamos ver um exemplo de como declarar e utilizar um array em C.

```c
// 10_arrays.c
#include <stdio.h>
int main() {
    int numeros[5]; // Declara um array de inteiros com 5 elementos
    printf("Informe 5 números inteiros:\n");

    // Lê os valores do usuário e armazena no array
    for (int i = 0; i < 5; i++) {
        scanf("%d", &numeros[i]);
    }

    // Exibe os valores armazenados no array
    printf("Os números informados foram:\n");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numeros[i]);
    }
    printf("\n");

    return 0;
}
```

Aqui temos bastante a observar! Primeiro, a declaração do array `numeros[5]` cria um array de inteiros com 5 elementos. Os arrays em C são indexados a partir de zero, ou seja, o primeiro elemento do array está na posição `0`, o segundo elemento está na posição `1`, e assim por diante. Isso significa que o último elemento do array `numeros` está na posição `4`, podemos dizer que a última posição de um array de `N` posições será `N-1`.

Agora vamos pensar sobre como acessar os elementos do array. No nosso exemplo, utilizamos um loop `for` para ler os valores do usuário e armazená-los no array. A variável `i` é usada como índice para acessar cada elemento do array. Quando chamamos `numeros[i]`, estamos acessando o elemento na posição `i` do array `numeros`. 

Os arrays podem ser multidimensionais, ou seja, podemos ter arrays com mais de uma dimensão. Isso é útil para representar matrizes ou tabelas de dados. Vamos ver um exemplo de como declarar e utilizar um array bidimensional em C.

```c
// 11_arrays_multidimensionais.c
#include <stdio.h>
int main() {
    int matriz[3][3]; // Declara um array bidimensional de inteiros 3x3
    printf("Informe os valores para a matriz 3x3:\n");

    // Lê os valores do usuário e armazena na matriz
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("Elemento [%d][%d]: ", i, j);
            scanf("%d", &matriz[i][j]);
        }
    }

    // Exibe os valores armazenados na matriz
    printf("A matriz informada é:\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matriz[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

Um prática bastante comum quando trabalhamos com arrays multidimensionais é utilizar loops aninhados para percorrer os elementos do array. No nosso exemplo, utilizamos dois loops `for` para ler os valores do usuário e armazená-los na matriz. O primeiro loop percorre as linhas da matriz, enquanto o segundo loop percorre as colunas. Quando acessamos um elemento da matriz, usamos a sintaxe `matriz[i][j]`, onde `i` é o índice da linha e `j` é o índice da coluna.

Os arrays podem ser utilizados como um tipo de dados enviado para funções. Isso permite que possamos passar um array como argumento para uma função e manipular seus valores dentro da função. Vamos ver um exemplo de como fazer isso:

```c
// 12_funcoes_com_arrays.c
#include <stdio.h>
// Função para calcular a média de um array de inteiros
double calcular_media(int numeros[], int tamanho) {
    int soma = 0;
    for (int i = 0; i < tamanho; i++) {
        soma += numeros[i];
    }
    return (double)soma / tamanho;
}

int main() {
    int numeros[5];
    printf("Informe 5 números inteiros:\n");

    // Lê os valores do usuário e armazena no array
    for (int i = 0; i < 5; i++) {
        scanf("%d", &numeros[i]);
    }

    // Calcula a média dos números informados
    double media = calcular_media(numeros, 5);
    printf("A média dos números informados é: %.2f\n", media);

    return 0;
}
```

Aqui temos um exemplo de como passar um array como argumento para uma função. A função `calcular_media` recebe um array de inteiros e o tamanho do array como parâmetros. Dentro da função, utilizamos um loop `for` para calcular a soma dos elementos do array e, em seguida, retornamos a média dos valores. No `main`, lemos os valores do usuário e chamamos a função `calcular_media` passando o array `numeros` e o tamanho do array como argumentos.

:::danger[Arrays não são dinâmicos]

Por padrão, os arrays em C têm tamanho fixo, ou seja, o tamanho do array é definido no momento da declaração e não pode ser alterado durante a execução do programa. Isso significa que precisamos ter cuidado ao trabalhar com arrays, para evitar acessar posições de memória fora dos limites do array, o que pode levar a comportamentos inesperados ou até mesmo a falhas de segmentação (segmentation fault).

Para trabalhar com arrays de tamanho dinâmico, podemos utilizar alocação dinâmica de memória, que veremos mais adiante. Por enquanto, é importante lembrar que os arrays em C são de tamanho fixo e precisamos ter cuidado ao acessá-los para evitar erros.

:::

:::danger[Arrays não podem ser retornados por funções]

Em C, não é possível retornar um array diretamente de uma função. Isso ocorre porque os arrays são tratados como ponteiros para o primeiro elemento do array, e retornar um ponteiro para um array pode levar a comportamentos inesperados. Em vez disso, podemos passar o array como argumento para a função e manipular seus valores dentro da função, ou ainda podemos retornar um ponteiro para o primeiro elemento do array alocado dinamicamente.

:::

Agora vamos ver um tipo de dado interessante para trabalhar com arrays, as strings.

## 8. Strings

Em C, não existe um tipo de dado específico para strings como em outras linguagens. Em vez disso, as strings são representadas como arrays de caracteres (`char`). Uma string é um array de caracteres que termina com o caractere nulo (`'\0'`), que indica o final da string. Vamos ver um exemplo de como declarar e utilizar uma string em C.

```c
// 13_strings.c
#include <stdio.h>
int main() {
    char nome[50]; // Declara uma string com tamanho máximo de 49 caracteres + 1 para o caractere nulo
    printf("Informe seu nome: ");
    scanf("%49s", nome); // Lê uma string do usuário, limitando a 49 caracteres

    printf("Olá, %s!\n", nome); // Exibe a string informada pelo usuário

    return 0;
}
```

Aqui temos um exemplo de como declarar e utilizar uma string em C. A string `nome` é declarada como um array de caracteres com tamanho máximo de 50, o que permite armazenar até 49 caracteres mais o caractere nulo (`'\0'`). Utilizamos a função `scanf` para ler a string do usuário, limitando a entrada a 49 caracteres para evitar overflow. Em seguida, exibimos a string informada pelo usuário utilizando o especificador `%s`. Outra forma de fazer essa leitura é utilizando a função `fgets`, que permite ler uma linha inteira, incluindo espaços em branco, até encontrar um caractere de nova linha (`'\n'`) ou atingir o tamanho máximo especificado.

```c
// 14_strings_fgets.c
#include <stdio.h>
int main() {
    char nome[50]; // Declara uma string com tamanho máximo de 49 caracteres + 1 para o caractere nulo
    printf("Informe seu nome: ");
    fgets(nome, sizeof(nome), stdin); // Lê uma linha inteira do usuário

    printf("Olá, %s", nome); // Exibe a string informada pelo usuário

    return 0;
}
```

Aqui utilizamos a função `fgets` para ler uma linha inteira do usuário, incluindo espaços em branco. A função `fgets` lê até o tamanho máximo especificado (neste caso, 50 caracteres) ou até encontrar um caractere de nova linha (`'\n'`). É importante lembrar que a função `fgets` inclui o caractere de nova linha na string lida, então, se necessário, podemos removê-lo manualmente.

```c
// 15_strings_remover_nova_linha.c
#include <stdio.h>
#include <string.h>
int main() {
    char nome[50]; // Declara uma string com tamanho máximo de 49 caracteres + 1 para o caractere nulo
    printf("Informe seu nome: ");
    fgets(nome, sizeof(nome), stdin); // Lê uma linha inteira do usuário

    // Remove o caractere de nova linha, se presente
    nome[strcspn(nome, "\n")] = '\0';

    printf("Olá, %s!\n", nome); // Exibe a string informada pelo usuário

    return 0;
}
```

Aqui utilizamos a função `strcspn` para encontrar a posição do caractere de nova linha na string e substituí-lo por um caractere nulo (`'\0'`), efetivamente removendo o caractere de nova linha da string. Outro ponto é a utiliza''cão da biblioteca `<string.h>`, que contém funções úteis para manipulação de strings, como `strcpy`, `strlen`, `strcmp`, entre outras.

| Função                                                  | Descrição                                                                              | Exemplo de uso                                                                |
| ------------------------------------------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `size_t strlen(const char *s)`                          | Retorna o número de caracteres antes do `'\0'` em `s`.                                 | `char s[] = "Olá"; printf("%zu\n", strlen(s)); // 3\n`                    |
| `char *strcpy(char *dest, const char *src)`             | Copia a string `src` (incluindo `'\0'`) para `dest`.                                   | `char a[10]; strcpy(a, "Mundo"); // a == "Mundo"\n`                      |
| `char *strncpy(char *dest, const char *src, size_t n)`  | Copia até `n` caracteres de `src` para `dest` (sem garantia de `'\0'` se `src` \>= `n`). | `char a[5]; strncpy(a, "ABCDEFG", 4); a[4] = '\0'; // "ABCD"\n`         |
| `char *strcat(char *dest, const char *src)`             | Concatena `src` ao fim de `dest` (deve haver espaço suficiente).                       | `char a[20] = "Hello, "; strcat(a, "World!"); // a == "Hello, World!"\n` |
| `char *strncat(char *dest, const char *src, size_t n)`  | Concatena até `n` caracteres de `src` ao fim de `dest`.                                | `char a[20] = "123"; strncat(a, "456789", 3); // a == "123456"\n`        |
| `int strcmp(const char *s1, const char *s2)`            | Compara lexicograficamente `s1` e `s2`; retorna \<0, 0, \>0.                             | `printf("%d\n", strcmp("A", "B")); // \<0\n`                                |
| `int strncmp(const char *s1, const char *s2, size_t n)` | Compara até `n` caracteres de `s1` e `s2`.                                             | `printf("%d\n", strncmp("ABC", "ABD", 2)); // 0\n`                         |
| `char *strchr(const char *s, int c)`                    | Retorna ponteiro para a primeira ocorrência de `c` em `s`, ou `NULL`.                  | `char *p = strchr("banana", 'n'); // p aponta para "nana"\n`              |
| `char *strrchr(const char *s, int c)`                   | Retorna ponteiro para a última ocorrência de `c` em `s`, ou `NULL`.                    | `char *p = strrchr("banana", 'a'); // p aponta para "a"\n`                |
| `char *strstr(const char *hay, const char *ndl)`        | Retorna ponteiro para a primeira substring `ndl` em `hay`, ou `NULL`.                  | `char *p = strstr("foobar", "oba"); // p aponta para "obar"\n`            |

:::danger[Strings não são arrays de caracteres]

Cuidado, strings não são arrays de caracteres! Elas são representadas como arrays de caracteres, mas possuem um comportamento diferente. As strings em C são terminadas com o caractere nulo (`'\0'`), que indica o final da string. Isso significa que, ao trabalhar com strings, precisamos ter cuidado para não acessar posições de memória fora dos limites da string, o que pode levar a comportamentos inesperados ou até mesmo a falhas de segmentação (segmentation fault).

:::

## 9. Ponteiros

Legal, até aqui vimos funções e arrays, conceitos que já nos permitem modularizar e armazenar coleções de dados. Mas C oferece um recurso ainda mais poderoso: os **ponteiros**, que são variáveis cujo valor é um endereço de memória. Por que entender ponteiros é importante? Porque, com eles, podemos:

* **Passar grandes estruturas** (arrays, structs) para funções sem copiar todo o conteúdo.
* **Manipular diretamente** a memória e construir estruturas dinâmicas (listas encadeadas, árvores).
* **Controlar a alocação dinâmica** de memória com `malloc` e `free`, criando buffers em tempo de execução.

De novo, vamos continuar com um programa pequeno, mas que ilustra vários usos de ponteiros. Veja um exemplo que troca valores, percorre um array com aritmética de ponteiros e imprime uma string literal:

```c
// 13_ponteiros.c
#include <stdio.h>

// Função que troca dois inteiros via ponteiros
void trocar(int *a, int *b) {
    int temp = *a;  // lê valor apontado por 'a'
    *a = *b;        // escreve valor apontado por 'b' em *a
    *b = temp;      // grava temp em *b
}

int main(void) {
    int x = 10, y = 20;
    int *px = &x;   // px aponta para x
    int *py = &y;   // py aponta para y

    printf("Antes: x = %d, y = %d\n", x, y);
    trocar(px, py); // passando endereços de x e y
    printf("Depois: x = %d, y = %d\n", x, y);

    // Percorrendo um array com ponteiro
    int arr[] = {1, 2, 3, 4, 5};
    int *p = arr;  // 'arr' decai para &arr[0]
    printf("Array: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", *(p + i)); // aritmética de ponteiro
    }
    printf("\n");

    // Imprimindo string literal via ponteiro
    char *s = "Olá, Mundo!";
    printf("String: %s\n", s);

    return 0;
}
```

Aqui cada ponteiro tem um papel:

* `int *px = &x;` e `int *py = &y;`
  Declaramos ponteiros para `int` e inicializamos com `&`, obtendo o endereço das variáveis `x` e `y`.
* Na função `trocar(int *a, int *b)`, os parâmetros são ponteiros. Dentro dela, usamos `*a` e `*b` para **ler** e **escrever** nos endereços passados, alterando `x` e `y` na chamada.
* `int *p = arr;` faz “decair” o array para um ponteiro ao primeiro elemento. Na expressão `*(p + i)`, somamos `i` ao ponteiro (avançamos `i` elementos) e depois desreferenciamos com `*`.
* `char *s = "Olá, Mundo!";` aponta para a primeira posição de uma string literal. O `%s` do `printf` percorre esse bloco até encontrar o caractere `'\0'`.

A sintaxe de ponteiros em C envolve:

* **Declaração**: `tipo *nome` (por exemplo, `int *p;`).
* **Operador `&`**: obtém o endereço de uma variável (ex.: `&x`).
* **Operador `*`**: desreferencia um ponteiro, acessando o valor apontado (ex.: `*p`).
* **Aritmética de ponteiros**: `p + n` anda `n` posições do tipo apontado por `p`.

:::danger[Cuidados com ponteiros]

Ponteiros são poderosos, mas também perigosos. Aqui estão alguns cuidados importantes:
* **Inicialização**: sempre inicialize ponteiros antes de usá-los. Ponteiros não inicializados podem apontar para locais aleatórios na memória, causando comportamento indefinido.
* **Acesso fora dos limites**: nunca acesse memória além do que foi alocado. Isso pode corromper dados ou causar falhas de segmentação.
* **Liberação de memória**: se você alocar memória dinamicamente com `malloc`, sempre libere com `free` para evitar vazamentos de memória.
* **Ponteiros nulos**: verifique se um ponteiro é nulo antes de desreferenciá-lo. Acessar um ponteiro nulo resulta em comportamento indefinido.
* **Evite ponteiros pendentes**: após liberar memória, evite usar o ponteiro que apontava para ela. Isso é conhecido como ponteiro pendente (dangling pointer) e pode levar a erros difíceis de depurar.

:::

Legal, falamos de alguns usos dos ponteiros, mas sempre acho que um exemplo visual facilita bastante nosso entendimento de como esses elementos são utilizados. Os ponteiros são tipos de variáveis especiais, pois o que eles armazenam não são outros valores, mas sim endereços de memória. 

<img src="https://www.cse.unr.edu/~sushil/class/cs202/notes/pointers/pointers/ptr1.gif" alt="Uso de ponteiros" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />
<br />

Quando observamos a imagem, podemos ver que as variáveis `ptr`, `num1` e `num2` ocupam as posições de memória `0500`, `0600` e `0604`, respectivamente. O ponteiro `ptr` armazena o endereço de memória da variável `num1`, que é `0600`. Quando desreferenciamos o ponteiro `ptr` com `*ptr`, estamos acessando o valor armazenado na posição de memória `0600`.

Um outro ponto bastante interessante de se observar é que os nomes das funções também são ponteiros. Quando declaramos uma função, o nome da função é um ponteiro para o endereço de memória onde a função está armazenada. Isso significa que podemos passar o nome da função como argumento para outra função, ou ainda podemos armazenar o endereço da função em um ponteiro de função. Vamos ver um exemplo disso:

```c
// extra_funcoes.c
#include <stdio.h>
// Função que recebe um ponteiro para uma função
void executar_funcao(void (*funcao)()) {
    funcao(); // Chama a função passada como argumento
}
// Função que será passada como argumento
void minha_funcao() {
    printf("Executando minha_funcao!\n");
}
int main() {
    // Passa o nome da função como argumento
    executar_funcao(minha_funcao);
    return 0;
}
```

Aqui temos um exemplo de como passar o nome de uma função como argumento para outra função. A função `executar_funcao` recebe um ponteiro para uma função que não recebe parâmetros e não retorna valor (`void (*funcao)()`). Dentro da função, chamamos a função passada como argumento. No `main`, passamos o nome da função `minha_funcao` como argumento para `executar_funcao`, que executa a função.

Agora vamos ver uma utilização poderoza dos ponteiros, que a alocação dinâmica de memória. Ela permite que nossos programas solicitem memória para o sistema operacional em tempo de execução! Mas para isso, precisamos compreender primeiro alguns tipos de memória que nossos programas utilizam.

## 10. Alocação dinâmica de memória

Para compreendermos a alocação dinâmica, precisamos entender os diferentes tipos de memória que nossos programas utilizam. Em C, a memória é dividida em quatro áreas principais:
1. ***Text Segment (ou Code Segment)***: Contém o código executável do programa (as instruções compiladas). Geralmente é somente-leitura e compartilhado entre processos que usam o mesmo binário.
2. ***Data Segment***:
    - **Initialized Data**: armazena variáveis globais e estáticas que você inicializa explicitamente.
    - **Uninitialized Data (BSS - Block Store by Symbol)**: armazena variáveis globais e estáticas não inicializadas (ou inicializadas a zero).
3. ***Heap***: Área de memória usada para alocação dinâmica em tempo de execução. Cresce “para cima” (endereços aumentam) conforme você chama malloc(), calloc() ou realloc(). Você deve liberar esses blocos manualmente com free(), caso contrário ocorre memory leak.
4. **Stack**: Área de memória usada para variáveis locais e contextos de chamada (frames de função). Cresce “para baixo” (endereços diminuem) cada vez que você entra em uma função, e é liberado automaticamente ao retornar. Tamanho limitado; ultrapassar chamando funções recursivas demais ou alocando arrays locais enormes pode causar stack overflow.

<img src="https://d8it4huxumps7.cloudfront.net/uploads/images/66267d4a18f3e_memory_allocation_process.jpg?d=2000x2000" alt="Regiões de Memória" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />
<br />

<iframe width="560" height="315" src="https://www.youtube.com/embed/2htbIR2QpaM?si=2yMVv3hIfh3Dixh4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::tip[Tamanho do Heap]

O heap de um programa C não é “infinito” – ele está sujeito a várias camadas de limite, que podem ser configuradas ou impostas pelo sistema operacional e pela própria arquitetura do processo:

1. **Espaço de endereçamento virtual**

   * Em **processos de 32 bits**, o heap só consegue crescer dentro dos \~3 GiB (ou \~2 GiB, em algumas configurações) de espaço virtual disponíveis por processo.
   * Em **processos de 64 bits**, o espaço virtual é tão grande (até exabytes) que, na prática, o limite passa a ser ditado pela memória física + swap + políticas do SO.

2. **Limites do sistema operacional**

   * No Linux/Unix, cada processo carrega um limite em bytes de “address space” definido por `RLIMIT_AS`. Você pode ver e ajustar esse valor com o shell:

     ```bash
     # mostra o limite atual (em kilobytes)
     ulimit -v
     # remove qualquer limite
     ulimit -v unlimited
     # limita o virtual memory a 1 GiB
     ulimit -v $((1024*1024))
     ```
   * Via **code**, é possível usar `setrlimit()` (em `<sys/resource.h>`) para abaixar ou erigir limites de heap/virtual antes de chamar `malloc()`.

3. **Cgroups e containers**

   * Em ambientes Linux modernos (Docker, systemd, Kubernetes), você pode agrupar processos em um cgroup e impor um máximo de memória (RAM + swap). Se o programa exceder esse limite, o kernel mata o processo (OOM).
   * Exemplos de configuração em `/sys/fs/cgroup/memory/.../memory.limit_in_bytes`.

4. **Políticas de Overcommit e Page-file (Windows)**

   * No Windows, o heap é limitado pelo tamanho do arquivo de paginação (“page file”) e pelas políticas de commit do sistema. Também é possível criar **Job Objects** e definir um máximo de memória virtual ou física para o conjunto de processos do Job.

5. **Configurações do allocador**

   * Muitos allocators (ptmalloc, jemalloc, tcmalloc) expõem variáveis de ambiente ou funções (`mallopt`, `je_*`) para controlar comportamento de arenas, zonas de mmap, threshold de liberação de memória, etc. Isso afeta performance e fragmentação, mas não altera o teto imposto pelo SO.

---

**Resumo**

* **Limite prático** = min( espaço de endereçamento, RLIMIT\_AS, memória física+swap, políticas de overcommit/cgroup/job ).
* **Configurável** via:

  * `ulimit -v` / `setrlimit(RLIMIT_AS)` no Unix,
  * cgroups em Linux moderno,
  * configurações de page file e Job Objects no Windows,
  * parâmetros do próprio allocator (mallopt, variáveis de ambiente).

:::

Legal, vamos bastante, mas cade um código para gente ver? Vamos lá!

Vamos ver um exemplo de alocação dinâmica de memória em C. Neste exemplo, vamos criar um programa que lê uma quantidade variável de números inteiros do usuário e os armazena em um array alocado dinamicamente.

```c
// 14_alocacao_dinamica.c
#include <stdio.h>
#include <stdlib.h> // Necessário para malloc e free
int main() {
    int n;
    printf("Quantos números você deseja informar? ");
    scanf("%d", &n);

    // Aloca memória dinamicamente para um array de inteiros
    int *numeros = (int *)malloc(n * sizeof(int));
    if (numeros == NULL) {
        printf("Erro ao alocar memória!\n");
        return 1; // Retorna 1 em caso de erro
    }

    // Lê os valores do usuário e armazena no array
    printf("Informe %d números inteiros:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &numeros[i]);
    }

    // Exibe os valores armazenados no array
    printf("Os números informados foram:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", numeros[i]);
    }
    printf("\n");

    // Libera a memória alocada
    free(numeros);

    return 0;
}
```

Aqui temos um exemplo de alocação dinâmica de memória. Utilizamos a função `malloc` para alocar memória para um array de inteiros com tamanho `n`, que é lido do usuário. A função `malloc` retorna um ponteiro para o início da memória alocada, que armazenamos na variável `numeros`. É importante verificar se a alocação foi bem-sucedida, verificando se o ponteiro retornado é diferente de `NULL`. Se a alocação falhar, exibimos uma mensagem de erro e retornamos um código de erro.
Depois de ler os valores do usuário e armazená-los no array, exibimos os valores armazenados. Por fim, utilizamos a função `free` para liberar a memória alocada, evitando vazamentos de memória.

:::danger[Alocação dinâmica de memória]

A alocação dinâmica de memória é uma ferramenta poderosa, mas deve ser usada com cuidado. Aqui estão alguns pontos importantes a serem lembrados:
* **Verifique se a alocação foi bem-sucedida**: sempre verifique se o ponteiro retornado por `malloc` não é `NULL`. Se for, significa que a alocação falhou e você deve tratar esse erro adequadamente.
* **Libere a memória alocada**: sempre libere a memória alocada com `free` quando não precisar mais dela. Isso evita vazamentos de memória, que podem levar a um consumo excessivo de memória e, eventualmente, a falhas do programa.
* **Cuidado com ponteiros pendentes**: após liberar a memória, evite usar o ponteiro que apontava para ela. Isso é conhecido como ponteiro pendente (dangling pointer) e pode levar a erros difíceis de depurar.

:::

Um último ponto importante sobre a alocação dinâmica de memória é que ela não precisa alocar apenas arrays. Podemos alocar qualquer tipo de dado, incluindo structs e outros tipos definidos pelo usuário. Mas além disso, ela não precisa alocar memória contígua, ou seja, podemos alocar blocos de memória de tamanhos diferentes e armazenar os ponteiros para esses blocos em um array ou lista. Isso nos permite criar estruturas de dados dinâmicas, como listas encadeadas, pilhas e filas.

## 11. Structs

Até aqui vimos como organizar dados simples (variáveis), coleções de dados homogêneos (arrays) e modularizar funções e acessar memória com ponteiros. Mas muitos problemas do mundo real exigem representar **objetos compostos**, com diversos campos de tipos diferentes — pense em um **ponto 2D** (x, y), em um **aluno** (nome, matrícula, notas) ou em um **nó de lista encadeada** (valor, próximo). É aí que entram as **structs**, que nos permitem agrupar múltiplos membros sob um único nome.

```c
// Definição de uma struct sem typedef
struct Ponto {
    int x;
    int y;
};

int main(void) {
    // Declaração de variável do tipo struct Ponto
    struct Ponto p1;
    p1.x = 10;
    p1.y = 20;
    printf("Ponto p1: (%d, %d)\n", p1.x, p1.y);
    return 0;
}
```

No exemplo acima, `struct Ponto` cria um novo **tipo composto** com dois campos `int`. Para simplificar a sintaxe, podemos usar `typedef`:

```c
// Definindo um alias com typedef
typedef struct {
    int x;
    int y;
} Ponto;

// Agora podemos declarar direto:
int main(void) {
    Ponto p2 = { .x = 5, .y = 15 }; // inicialização por designador
    printf("Ponto p2: (%d, %d)\n", p2.x, p2.y);
    return 0;
}
```

### Exemplos de uso

1. **Array de structs**
   Agrupar vários registros em um único vetor.

   ```c
   typedef struct {
       char nome[50];
       int idade;
   } Pessoa;

   Pessoa sala[3] = {
       { "Alice", 20 },
       { "Bruno", 22 },
       { "Carla", 19 }
   };
   // Acessando:
   printf("%s tem %d anos\n", sala[1].nome, sala[1].idade);
   ```

2. **Ponteiro para struct e alocação dinâmica**
   Útil quando o número de elementos só é conhecido em tempo de execução.

   ```c
   Pessoa *grupo = malloc(n * sizeof *grupo);
   if (!grupo) exit(1);
   // Preenchendo:
   strcpy(grupo[0].nome, "Diego");
   grupo[0].idade = 21;
   // …
   free(grupo);
   ```

3. **Struct aninhada**
   Podemos ter structs dentro de structs para modelar hierarquias.

   ```c
   typedef struct {
       int dia, mes, ano;
   } Data;

   typedef struct {
       char titulo[100];
       Data lancamento;
       float nota;
   } Filme;

   Filme f = {
       "Meu Filme",
       { .dia = 1, .mes = 7, .ano = 2025 },
       8.5f
   };
   printf("%s (%02d/%02d/%04d): %.1f\n",
          f.titulo, f.lancamento.dia, f.lancamento.mes,
          f.lancamento.ano, f.nota);
   ```

---

Com as **structs**, você organiza dados relacionados de forma elegante e sem perder a eficiência de C. O uso de `typedef` torna o código mais legível, eliminando a necessidade de escrever `struct` a todo momento. Em programas maiores, structs formam a base para criar **listas encadeadas**, **árvores**, **hash tables** e outras estruturas dinâmicas que habilitam sistemas complexos e modulares.

Quando você tem um **ponteiro** para uma `struct`, o operador `->` é a forma mais direta de acessar seus campos, equivalendo a `(*ponteiro).campo` mas com sintaxe mais limpa.

```c
#include <stdio.h>

typedef struct {
    int id;
    char nome[20];
} Aluno;

int main(void) {
    Aluno a = { .id = 123, .nome = "Maria" };
    Aluno *pa = &a;  // ponteiro para a struct

    // Acesso via operador '->'
    printf("Aluno %d: %s\n", pa->id, pa->nome);
    // equivale a:
    // printf("Aluno %d: %s\n", (*pa).id, (*pa).nome);

    return 0;
}
```

* **Declaração**: `Aluno *pa = &a;` faz `pa` apontar para `a`.
* **Uso de `->`**: `pa->id` lê `a.id`; `pa->nome` lê `a.nome`.

---

Para criar instâncias de `struct` em tempo de execução, usamos o **heap** com `malloc` e liberamos com `free`. Assim, não ficamos restritos ao escopo de variáveis locais:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    int id;
    char nome[20];
} Aluno;

int main(void) {
    // Aloca um único struct Aluno
    Aluno *pa = malloc(sizeof *pa);
    if (!pa) {
        perror("malloc falhou");
        return 1;
    }

    // Preenche via ponteiro e '->'
    pa->id = 456;
    strcpy(pa->nome, "João");

    printf("Aluno alocado: %d - %s\n", pa->id, pa->nome);

    free(pa);  // devolve memória ao heap

    // Alocando um vetor de 3 structs Aluno
    size_t n = 3;
    Aluno *vet = malloc(n * sizeof *vet);
    if (!vet) {
        perror("malloc falhou");
        return 1;
    }

    // Inicialização simples
    for (size_t i = 0; i < n; i++) {
        vet[i].id = i + 1;
        snprintf(vet[i].nome, sizeof vet[i].nome, "Aluno%zu", i + 1);
    }

    // Impressão
    for (size_t i = 0; i < n; i++) {
        printf("vet[%zu]: %d - %s\n", i, vet[i].id, vet[i].nome);
    }

    free(vet);  // libera o array de structs
    return 0;
}
```

* **`malloc(sizeof *pa)`**: aloca exatamente o tamanho de `*pa` (mais seguro contra mudanças de tipo).
* **`free(pa)`**: liberta a memória alocada.
* No **vetor**, usamos `vet[i].campo`; poderíamos também usar `(vet + i)->campo` para ilustrar novamente o `->`.

Com isso, você pode criar tanto uma única instância quanto coleções de structs em heap, controlando manualmente o tempo de vida dos objetos e evitando limitações de escopo de funções.

## 12. Arquivos

Para finalizar nossa jornada, vamos falar sobre **arquivos**. Em C, podemos ler e escrever dados em arquivos usando funções da biblioteca `<stdio.h>`. Isso nos permite persistir dados entre execuções do programa, o que é essencial para muitas aplicações. Em C, todo acesso a arquivos em disco é feito via ponteiros do tipo `FILE*`. Isso nos permite **ler**, **escrever** e **navegar** em arquivos de texto ou binários, mantendo o código organizado e portátil.

- Abrindo e fechando arquivos

```c
#include <stdio.h>

FILE *f = fopen("arquivo.txt", "r");  // abre para leitura
if (!f) {
    perror("fopen");
    return 1;
}

/* … uso de f … */

fclose(f);  // fecha e libera recursos
```

* Modos comuns de abertura:

  * `"r"`  – leitura (erro se não existir)
  * `"w"`  – escrita (cria/trunca)
  * `"a"`  – escrita em modo append
  * `"r+"` – leitura/escrita sem truncar
  * Acrescente `"b"` para arquivos binários (`"rb"`, `"wb"`, …).

- Escrevendo em arquivos de texto

```c
#include <stdio.h>

int main(void) {
    FILE *fw = fopen("saida.txt", "w");
    if (!fw) { perror("fopen"); return 1; }

    fprintf(fw, "ID: %d\nNome: %s\n", 42, "Fulano");
    fprintf(fw, "Nota1: %.1f, Nota2: %.1f\n", 7.5, 8.0);

    fclose(fw);
    return 0;
}
```

* **`fprintf`** funciona como `printf`, mas envia saída para o `FILE*`.

- Lendo de arquivos de texto

```c
#include <stdio.h>

int main(void) {
    FILE *fr = fopen("saida.txt", "r");
    if (!fr) { perror("fopen"); return 1; }

    int id;
    char nome[50];
    float n1, n2;

    // lê valores formatados
    if (fscanf(fr, "ID: %d\nNome: %49[^\n]\n", &id, nome) == 2) {
        printf("Lido: %d - %s\n", id, nome);
    }

    // pula até o próximo par de notas
    fscanf(fr, "Nota1: %f, Nota2: %f\n", &n1, &n2);
    printf("Notas: %.1f, %.1f\n", n1, n2);

    fclose(fr);
    return 0;
}
```

* **`fscanf`** funciona como `scanf` mas lê de um `FILE*`.
* Para ler linhas inteiras (inclusive espaços), use **`fgets(buf, tamanho, fr)`**.

- Arquivos binários

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int id;
    float nota;
} Registro;

int main(void) {
    Registro r = { 123, 9.5f };

    // grava binário
    FILE *fb = fopen("dados.bin", "wb");
    if (!fb) { perror("fopen"); return 1; }
    fwrite(&r, sizeof r, 1, fb);
    fclose(fb);

    // lê binário
    FILE *fr = fopen("dados.bin", "rb");
    if (!fr) { perror("fopen"); return 1; }
    Registro r2;
    if (fread(&r2, sizeof r2, 1, fr) == 1) {
        printf("Registro lido: id=%d, nota=%.1f\n", r2.id, r2.nota);
    }
    fclose(fr);
    return 0;
}
```

* **`fwrite(ptr, tamanho, count, FILE*)`** e **`fread`** manipulam blocos de bytes, ideal para structs ou buffers de dados.

- Movendo o cursor no arquivo

* **`fseek(FILE *f, long offset, int whence)`**: desloca o ponteiro de leitura/escrita.

  * `SEEK_SET` (início), `SEEK_CUR` (posição atual), `SEEK_END` (final).
* **`ftell(FILE *f)`**: retorna posição atual (em bytes).
* **`rewind(FILE *f)`**: volta ao início (`fseek(f, 0, SEEK_SET)`).

---

Com essas funções, você tem controle completo sobre como seus programas armazenam e recuperam dados de arquivos, seja em formato legível (texto) ou eficiente (binário), aproveitando alocação dinâmica e estruturas compostas conforme necessário.


## 13. Referências

- The C Book: [Link](https://publications.gbdirect.co.uk/c_book/)
- C Programming Language (Kernighan & Ritchie): [Link](https://www.amazon.com.br/Programming-Language-2nd-Brian-Kernighan/dp/0131103628)
- Linguagem C, completa e descomplicada: [Link](https://www.amazon.com.br/Linguagem-C-ANDR%C3%89-BACKES/dp/8535291067/ref=sr_1_1?dib=eyJ2IjoiMSJ9.FO_0tltZNLAHMWWsdEODmYVp488WvSOlFBNaLbkLZF0.oGpnIcLDADUw2ckSwxtWHfohb7X34caELPu8JAt7fJg&dib_tag=se&keywords=c+completo+e+descomplicado&qid=1748338536&sr=8-1&ufe=app_do%3Aamzn1.fos.fcd6d665-32ba-4479-9f21-b774e276a678)
- Introdução à programação com a linguagem C: [Link](https://www.amazon.com.br/Introdu%C3%A7%C3%A3o-Programa%C3%A7%C3%A3o-com-Linguagem-Problemas/dp/8575224859/ref=sr_1_2?__mk_pt_BR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=3IQ65V7OA8AD4&dib=eyJ2IjoiMSJ9.tAXgIoOizXb9qgL6gnCgOWXy-9dMzqpMHcpn16yQzjifCTyLkJpLnlUJ0F0GsaI1Vv3tSlTw01Tr6m3LY1Usy_5YWlQcpNr4nOh0V6wzezBZSWX9d9QRu7YWWA6Owq1ZRgkBjpFYUzqd9BCoWruMr8t6PEP23Bp8fTojGyLGlXKGxE0HrpxOROfYUd7KxyxPXR0KZb6IjbH7WEEM53_GnKDOjO6Tgs1qD6zbZ8_S45oF20K4p_5kwSi_Ar3c3fOPlaB22XXpxrRFs9HNzmuBNUaDS36flHcCozIxA4Qvd3Y.qDM0VbKMlXnxdRntqH_XVMcLgL-zY1_ena_znvOGTmI&dib_tag=se&keywords=Introdu%C3%A7%C3%A3o+%C3%A0+programa%C3%A7%C3%A3o+com+a+linguagem+C&qid=1748338587&sprefix=c+completo+e+descomplicado%2Caps%2C227&sr=8-2&ufe=app_do%3Aamzn1.fos.6d798eae-cadf-45de-946a-f477d47705b9)
- Use a cabeça! C: [Link](https://www.amazon.com.br/Use-cabe%C3%A7a-C-David-Griffiths/dp/8576087944/ref=sr_1_2?__mk_pt_BR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=2KY9X2P4MY2L4&dib=eyJ2IjoiMSJ9.GaaDwrfW2ltm_27Wwu6rY_4f27RcUzr_yPRcOnpKTvuliIXBtrJUknDPqRPz4wObaNQfPOWCgkSbAg9uV0PAlAHzU6lXermE7RDnDJIXTTLMQYVA3NKjhy7IPpSALsgW7xH9tskcLaqZsiDZMabdewIvxo20E4UpWhV2-A51piVjpCG08X5TSJOUcTjVlK7RBcsT8Yfmy-qaMl4Gcsfg3TpD7ISNhgAQ-123Wp1L51OSmbQ3WJcuJcLEMM77i5eTgwVkbWvMZJE6A9T6qftoWcaMePTvVA3bQu5wYEkgSmw.daVuf2czEKGddp1T2EkZKEvy65RWgfezWuWMond8_GQ&dib_tag=se&keywords=use+a+cabe%C3%A7a+c&qid=1748338625&sprefix=use+a+cabeca+%2Caps%2C264&sr=8-2) 

<iframe width="560" height="315" src="https://www.youtube.com/embed/Gp2m8ZuXoPg?si=WpWgAsIFv0LVfiZ-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

<iframe width="560" height="315" src="https://www.youtube.com/embed/U3aXWizDbQ4?si=6CdYzgRBAlo2oIws" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

## 14. Exercícios

Pessoal, aqui vou colocar alguns exercícios para vocês praticarem tudo que conversamos até aqui! Eles vão de nível básico até um pouco mais avançado!

1. Soma de dois inteiros: Leia dois números inteiros do teclado e mostre sua soma.

2. Produto de float e int: Leia um número real (float) e um inteiro, calcule e exiba o produto.

3. Área de um círculo: Leia o raio (tipo double) de um círculo e calcule a área (π·r²), exibindo com duas casas decimais.

4. Par ou ímpar: Leia um inteiro e informe se ele é par ou ímpar (usando if/else).

5. Positivo, negativo ou zero: Leia um inteiro e diga se ele é positivo, negativo ou zero.

6. Maior de três números: Leia três inteiros e determine qual deles é o maior (apenas com if/else).

7. Conceito de nota: Leia uma nota (0–100) e atribua um conceito A/B/C/D/F segundo faixas predefinidas (ex.: ≥90 → A, ≥80 → B etc.).

8. Nome do mês: Leia um número de 1 a 12 e imprima o nome do mês correspondente (use switch).

9. Contagem até N: Leia um inteiro positivo N e imprima todos os números de 1 até N (laço for).

10. Soma de 1 a N: Leia N e calcule a soma de todos os inteiros entre 1 e N (pode usar while ou for).

11. Fatorial de N: Leia um inteiro N ≥ 0 e calcule seu fatorial usando um loop.

12. Série de Fibonacci: Leia um inteiro N e imprima os primeiros N termos da sequência de Fibonacci (0, 1, 1, 2, 3…).

13. Média de N valores: Leia N, depois leia N valores reais e exiba a média aritmética.

14. Tabuada de um número: Leia um inteiro X e imprima sua tabuada de 1 a 10.

15. Matriz e transposta: Leia o tamanho n (≤10), depois leia uma matriz quadrada n×n e mostre sua transposta.

16. Função max(a,b): Implemente uma função int max(int a, int b) que retorne o maior de dois inteiros e use-a para comparar dois valores lidos.

17. Função fatorial(n): Crie uma função long fatorial(int n) e utilize-a para mostrar o fatorial de um número lido.

18. Função recursiva de Fibonacci: Escreva uma função recursiva int fib(int n) e exiba o n-ésimo termo lido do usuário.

19. Verificador de número primo: Implemente uma função int eh_primo(int x) que retorne 1 se x for primo ou 0 caso contrário; depois, leia um valor N e liste todos os primos de 2 até N.

20. Utilizando ponteiros: Crie um programa que leia um número inteiro e utilize ponteiros para calcular o dobro e o triplo desse número, exibindo os resultados.

21. Alocação dinâmica de memória: Implemente um programa que leia N números inteiros, aloque dinamicamente um array para armazená-los e calcule a média desses números.

22. Structs: Defina uma struct para representar um aluno (com nome, matrícula e nota) e implemente um vetor para armazenar vários alunos, permitindo adicionar, remover e listar alunos.

A partir daqui os exercícios são um pouco mais robustos e exigem um pouco mais de reflexão, mas não se preocupe, você vai conseguir!

23. Gerenciamento de Estoque de Loja com `struct` e Alocação Dinâmica

Você vai implementar em C um **sistema de gerenciamento de estoque** para uma pequena loja, utilizando `struct` para representar cada produto e um **vetor dinâmico** para armazenar esses produtos em memória. Seu programa deverá prover um **menu interativo** com as seguintes funcionalidades mínimas:

- **Definição das Estruturas**

   * `typedef struct {  
       int codigo;           // identificador único do produto  
       char nome[50];        // nome do produto  
       char categoria[30];   // categoria ou departamento  
       float preco;          // preço unitário  
       int quantidade;       // unidades em estoque  
       int estoque_minimo;   // nível mínimo para reabastecimento  
     } Produto;`
   * Use um **vetor de `Produto`** alocado com `malloc`/`realloc`, de forma que seu programa possa crescer conforme novos itens sejam cadastrados.

- **Menu de Operações**
   Implemente um laço que exiba opções como:

   ```
   1) Cadastrar novo produto
   2) Remover produto (por código)
   3) Atualizar estoque (entrada/saída de mercadorias)
   4) Listar todos produtos
   5) Listar produtos abaixo do estoque mínimo
   6) Consultar produto (por código ou nome)
   7) Calcular valor total do estoque
   0) Sair
   ```

   Cada opção deve chamar uma **função** específica, recebendo ponteiro para o vetor e seu tamanho atual, e retornar — se necessário — o novo tamanho (após remoções ou inclusões).

- **Requisitos Funcionais**

   * **Cadastrar produto**: ler todos os campos e inserir no fim do vetor (use `realloc` para expandi-lo).
   * **Remover produto**: localizar pelo `codigo`, deslocar os elementos seguintes para “fechar o buraco” e reduzir o tamanho com `realloc`.
   * **Atualizar estoque**: pedir código, ler quantidade (+ para entrada, – para saída) e ajustar `quantidade` mantendo-a ≥ 0.
   * **Listagens**:

     * **Todos os produtos**: exibir tabela com `codigo`, `nome`, `categoria`, `preco`, `quantidade`.
     * **Estoque baixo**: listar apenas itens em que `quantidade < estoque_minimo`.
   * **Consulta**: buscar por código (igual) ou nome (substring com `strstr`), exibindo detalhes completos.
   * **Valor total do estoque**: somar, para cada produto, `preco * quantidade` e imprimir o resultado.

- **Persistência (opcional, nível avançado)**

   * Ao iniciar, ler um arquivo binário “estoque.dat” com a lista de produtos (`fread`).
   * Ao sair, gravar o vetor atualizado em “estoque.dat” (`fwrite`), garantindo que, ao reiniciar, os dados anteriores sejam restaurados.

- **Boas-práticas e Observações**

   * Modularize seu código em funções com assinatura clara (use `typedef` para apelidar ponteiros a funções, se desejar).
   * Verifique retornos de `malloc`/`realloc` e de operações de arquivo antes de usar os ponteiros.
   * Use `->` apenas quando trabalhar com ponteiros para `Produto`; para o vetor, use notação `vet[i].campo`.
   * Trate entradas inválidas (códigos não encontrados, quantidades negativas, limites de buffer em `scanf`).

---

