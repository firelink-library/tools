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

