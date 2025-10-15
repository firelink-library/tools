---
title: Instalando o Java JDK e uma IDE de Desenvolvimento
sidebar_position: 1
slug: /instalando-java
---

Nesta seção vamos abordar o processo de instalação do Java e vamos utilizar ele para realizar nossos estudos. Vamos compreender também como ele pode ser utilizado com algumas IDEs e o processo de compilação de um programa Java.

## 1. O que é o Java?

Vamos para algumas definições aqui primeiro:

> *Java is a programming language and computing platform first released by Sun Microsystems in 1995. It has evolved from humble beginnings to power a large share of today’s digital world, by providing the reliable platform upon which many services and applications are built. New, innovative products and digital services designed for the future continue to rely on Java, as well. While most modern Java applications combine the Java runtime and application together, there are still many applications and even some websites that will not function unless you have a desktop Java installed. Java.com, this website, is intended for consumers who may still require Java for their desktop applications – specifically applications targeting Java 8. Developers as well as users that would like to learn Java programming should visit the dev.java website instead and business users should visit oracle.com/java for more information.* - [Oracle, 2025](https://www.java.com/en/download/help/whatis_java.html)

> *Legal, mas Murilão, o que isso quer dizer?*

Ótima pergunta! O que temos aqui é um pouco da história do Java em um paragrafo bem longo. Vamos pegar algumas coisas aqui: Java foi criado em 1995 pela Sun Microsystems, em 1995. Naquela época, o Java foi criado com uma premissa maior:

`Write-Once, Run-Anywere`

> *Calma lá Murilão, eu vi aqui que a linguagem foi criada em 1991 por um cara chamada James Gosling. E o que quer dizer isso de escrever uma vez só e rodar em todo lugar?*

Vamos por partes. Sim, o criador da linguagem foi o James Gosling. Diga-se de passagem, esse senhor é responsável por diversas outras contribuições para a computação. Para ver mais sobre a história dele, verificar sua [bibliografia](https://computerhistory.org/profile/james-gosling/).

<img 
  src="https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQBIsf645xEhpk3gnJzE469py2axGGALfn_G5iexOTF902JWtbNSo_N1T7YKSZT9vME8USwjHiMiFQSPBZ3f-ltTcfono4nQIJ_dQfDOQ"
  alt="Use a Cabeça! Java"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>

Mas vamos lá, história do criador a parte, vamos compreender o cenário que estava o desenvolvimento de software em 1991, para compreender o porque a afirmação de escrever uma vez e rodar em todo lugar é muito importante. A programação estava surgindo em diversos locais, além dos datacenters. Diversos outros sistemas digitais, desde computadores pessoais, trens, e outros dispositivos programáveis estavam crescendo ao redor do mundo.

A forma como estes dispositivos lidavam com algumas complexidades, como os bits menos significativos ao realizar uma divisão não apresentavam um comportamento padrão. Por mais irrelevante que isso possa parecer, um erro de aproximação em um sistema crítico pode ter consequências bastante graves, envolvendo até mesmo a segurança das pessoas. Com as ferramentas que estavam disponíveis na época, era fácil cometer erros e possuíam um grande tempo para sua correção.

Mas calma, não acredite só no que eu estou falando (escrevendo)! Veja nas palavras do criador:

<iframe width="560" height="315" src="https://www.youtube.com/embed/6iP376VwcjY?si=NIpI3qke2vW80MRq" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }}></iframe>


## 2. Como o Java funciona?

Segundo a IBM, podemos dizer que:

> *O Java é uma tecnologia que usa tanto uma linguagem de programação quanto uma plataforma de software. Para criar uma aplicação usando o Java, você precisa baixar o Java Development Kit (JDK), que está disponível para Windows, macOS e Linux®. Você escreve o programa na linguagem de programação Java e, então, um compilador transforma o programa em bytecode Java — o conjunto de instruções para a Virtual Machine Java (JVM), que faz parte do ambiente de execução Java (JRE). O bytecode Java é executado sem modificação em qualquer sistema compatível com JVMs, permitindo que seu código Java seja executado em qualquer lugar. A plataforma de software Java consiste na JVM, na API Java e em um ambiente de desenvolvimento completo. A JVM analisa e executa ou interpreta o bytecode Java. A API Java compreende um amplo conjunto de bibliotecas que incluem objetos básicos, funções de rede e segurança, geração de xtensible Markup Language (XML) e serviços da web. Juntas, a linguagem Java e a plataforma de software Java criam uma tecnologia poderosa e comprovada para o desenvolvimento de software corporativo.* - [IBM, 2025](https://www.ibm.com/br-pt/think/topics/java)

Legal, agora vamos analisar o que aconteceu aqui: até o 

O fluxo do desenvolvimento com o Java é o seguinte:

1. Escrevemos nosso código-fonte em Java (arquivos *.java);
2. Utilizamos o compilador para analisar nosso código-fonte e gerar nosso arquivo de saída. No caso do Java, a saída do compilador é o `bytecode` que pode ser interpretado pelo próximo elemento do processo.
3. A nossa máquina virtual Java (JVM - Java Virtual Machine) vai interpretar o `bytecode` para executar o programa. Cada sistema vai possuir um Java Virtual Machine dedicada para ele.

Da etapa `1` para `2`, nosso arquivo passa de um arquivo `*.java` para um arquivo `*.class`. Esse arquivo `*.class` é o *bytecode* que será interpretado pela JVM.

<img 
  src="https://miro.medium.com/1*qQDHWG33fU2RQPNqd90unQ.jpeg"
  alt="Compilando e Executando um Programa Java"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>
<p align="center">Retirado de (https://miro.medium.com/1*qQDHWG33fU2RQPNqd90unQ.jpeg)</p>


> *Mas o Java não é lento? Eu ouvi falar bastante sobre isso.*

Boa colocação. De fato, o Java era bastante lento para ser executado. As grandes evoluções aconteceram na JVM, ela sofreu diversas otimizações para melhorar o desempenho da execução do código. Mas existe diferença na quantidade de memória utilizada pelos programas em Java que quando comparado com outras tecnologias (Rust, Go por exemplo).

<iframe width="560" height="315" src="https://www.youtube.com/embed/cAoymPToQdg?si=Y8mIPoGFOybc5DNi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }}></iframe>

Vamos agora iniciar a nossa etapa de programação?

## 3. Instalando a JDK

Desde que a Sun foi comprada pela Oracle, o JDK da Oracle não é mais open-source nas suas versões mais recentes. Contudo, podemos utilizar algumas alternativas ao JDK da Oracle, por exemplo o JDK da Amazon, o [Corretto](https://aws.amazon.com/pt/corretto/). Vamos primeiro realizar o download do Corretto. Vamos utilizar a versão mais recente do JDK que for LTS (em 2025, a versão 21).

Depois seguir com o procedimento de instalação de acordo com o seu respectivo sistema operacional. Vamos testar se o Java foi corretamente instalado e adicionado no PATH do sistema, digitando o seguinte comando no terminal:

```sh
java --version
```

O resultado deve ser o seguinte:

```sh
openjdk 21.0.8 2025-07-15 LTS
OpenJDK Runtime Environment Corretto-21.0.8.9.1 (build 21.0.8+9-LTS)
OpenJDK 64-Bit Server VM Corretto-21.0.8.9.1 (build 21.0.8+9-LTS, mixed mode, sharing)
```

Beleza, temos agora nossa JDK instalada. Vamos verificar agora se ela está funcionando corretamente. Para isso, vamos criar um primeiro arquivo fonte Java. Para o Java, cada arquivo fonte contem a definição de uma classe e deve possuir o mesmo nome desta classe.

```java
// Criando um primeiro arquivo em Java
public class OlaMundo {
  public static void main(String[] args){
    System.out.println("Ola Mundo Java!");
    System.out.println("Ainda bem que pouco verborrágico!");
  }
}
```

Agora vamos compilar nosso programa:

```sh
javac OlaMundo.java
```

O compilador vai produzir um arquivo chamado `OlaMundo.class`, que é o nosso bytecode compilado. Podemos inspecionar esse bytecode com o comando:

```sh
javap -c OlaMundo.class
```

Isso vai descompilar o arquivo e trazer ele em um formato inteligível para nós lermos. Agora, mas interessante é utilizar o seguinte comando:

```sh
xxd OlaMundo.class
```

O `xxd` vai fazer um dump do hexadecimal do arquivo. Vamos obter a seguinte saída:

```sh
00000000: cafe babe 0000 0041 001f 0a00 0200 0307  .......A........
00000010: 0004 0c00 0500 0601 0010 6a61 7661 2f6c  ..........java/l
00000020: 616e 672f 4f62 6a65 6374 0100 063c 696e  ang/Object...<in
00000030: 6974 3e01 0003 2829 5609 0008 0009 0700  it>...()V.......
00000040: 0a0c 000b 000c 0100 106a 6176 612f 6c61  .........java/la
00000050: 6e67 2f53 7973 7465 6d01 0003 6f75 7401  ng/System...out.
00000060: 0015 4c6a 6176 612f 696f 2f50 7269 6e74  ..Ljava/io/Print
00000070: 5374 7265 616d 3b08 000e 0100 0f4f 6c61  Stream;......Ola
00000080: 204d 756e 646f 204a 6176 6121 0a00 1000   Mundo Java!....
00000090: 1107 0012 0c00 1300 1401 0013 6a61 7661  ............java
000000a0: 2f69 6f2f 5072 696e 7453 7472 6561 6d01  /io/PrintStream.
000000b0: 0007 7072 696e 746c 6e01 0015 284c 6a61  ..println...(Lja
000000c0: 7661 2f6c 616e 672f 5374 7269 6e67 3b29  va/lang/String;)
000000d0: 5608 0016 0100 2241 696e 6461 2062 656d  V....."Ainda bem
000000e0: 2071 7565 2070 6f75 636f 2076 6572 626f   que pouco verbo
000000f0: 7272 c3a1 6769 636f 2107 0018 0100 084f  rr..gico!......O
00000100: 6c61 4d75 6e64 6f01 0004 436f 6465 0100  laMundo...Code..
00000110: 0f4c 696e 654e 756d 6265 7254 6162 6c65  .LineNumberTable
00000120: 0100 046d 6169 6e01 0016 285b 4c6a 6176  ...main...([Ljav
00000130: 612f 6c61 6e67 2f53 7472 696e 673b 2956  a/lang/String;)V
00000140: 0100 0a53 6f75 7263 6546 696c 6501 000d  ...SourceFile...
00000150: 4f6c 614d 756e 646f 2e6a 6176 6100 2100  OlaMundo.java.!.
00000160: 1700 0200 0000 0000 0200 0100 0500 0600  ................
00000170: 0100 1900 0000 1d00 0100 0100 0000 052a  ...............*
00000180: b700 01b1 0000 0001 001a 0000 0006 0001  ................
00000190: 0000 0001 0009 001b 001c 0001 0019 0000  ................
000001a0: 0031 0002 0001 0000 0011 b200 0712 0db6  .1..............
000001b0: 000f b200 0712 15b6 000f b100 0000 0100  ................
000001c0: 1a00 0000 0e00 0300 0000 0300 0800 0400  ................
000001d0: 1000 0500 0100 1d00 0000 0200 1e         .............
```

Todo bytecode de Java é iniciado com a expressão `cafe babe`. A explicação do criador da linguagem para isso é:

> *We used to go to lunch at a place called St Michael’s Alley. According to local legend, in the deep dark past, the Grateful Dead used to perform there before they made it big. It was a pretty funky place that was definitely a Grateful Dead Kinda Place. When Jerry died, they even put up a little Buddhist-esque shrine. When we used to go there, we referred to the place as Cafe Dead. Somewhere along the line, it was noticed that this was a HEX number. I was re-vamping some file format code and needed a couple of magic numbers: one for the persistent object file, and one for classes. I used CAFEDEAD for the object file format, and in grepping for 4 character hex words that fit after “CAFE” (it seemed to be a good theme) I hit on BABE and decided to use it. At that time, it didn’t seem terribly important or destined to go anywhere but the trash can of history. So CAFEBABE became the class file format, and CAFEDEAD was the persistent object format. But the persistent object facility went away, and along with it went the use of CAFEDEAD – it was eventually replaced by RMI.*

Mas ainda não executamos nosso arquivo compilado! Vamos fazer com o comando:

```sh
java OlaMundo
```

E vamos ter a saída:

```sh
Ola Mundo Java!
Ainda bem que pouco verborrágico!
```

Beleza! Agora temos como compilar nossos programas escritos em Java!
Recomendo muito a utilização de alguma IDE ou editor de texto para criar os programas. Minha sugestão é utilizar o IntelliJ da JetBrains.

> *Mas Murilão, não posso só utilizar o VS Code?*

Pode sim! É uma boa escolha também. Contudo, o IntelliJ tem uma versão gratuita, a Community Edition. Eu recomendo bastante sua utilização para ver, em minha opinião, uma das melhores ferramentas já desenvolvidas para auxiliar durante o processo de programação. Fica o [link](https://www.jetbrains.com/idea/download/).

## 4. Recomendação de Material em Vídeo

Pessoal esse material não é meu, mas recomendo fortemente, dada a qualidade e profundidade com que os conceitos são apresentados:

<iframe width="560" height="315" src="https://www.youtube.com/embed/sTX0UEplF54?si=_bc5OEiqyAI9EM6A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }}></iframe>