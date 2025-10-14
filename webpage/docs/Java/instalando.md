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

Desde que a Sun foi comprada pela Oracle, o JDK da Oracle não é mais open-source nas suas versões mais recentes. Contudo, podemos utilizar algumas alternativas ao JDK da Oracle, por exemplo o JDK da Amazon, o [Corretto](https://aws.amazon.com/pt/corretto/). Vamos primeiro realizar o download do 