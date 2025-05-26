---
title: Ferramentas, Compiladores e Ambientes de Desenvolvimento
sidebar_position: 1
slug: /c-lang-tools
---


Aqui pessoal vamos analisar algumas ferramentas e o processo de compilação de código.

## 1. Origem da compilação de código

Vamos avaliar algumas coisas antes de iniciarmos nosso estudo. Primeiro vamos compreender como os programas de computador são criados e executados por nossas máquinas. Primeiro, nosso processador é uma máquina capaz de compreender um conjunto de instruções, chamadas de código de máquina. Essas instruções são responsáveis por executar oeprações a nível do processador, como ler e escrever em posições de memória, mover dados entre registradores, realizar operações ariteméticas e lógicas, para citar algumas.


:::tip[Como os processadores compreendem as instruções]

<iframe width="560" height="315" src="https://www.youtube.com/embed/vqs_0W-MSB0?si=qHdCGD0GVPTBPcvJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

> "Murilão, beleza, até aqui você falou bonito, deu para compreender que o processador compreende um conjunto de instruções e executa umas operações. Mas onde a programação entre ai?"

Ótima pergunta! Vamos avaliar onde nossos programas entre nessa história toda. O processador carrega as instruções e os operandos dessas instruções de endereços de memória. Agora, nossos programas são responsáveis por fornecer essas instruções e operandos. Para isso vamos verificar algumas formas de fazer isso.

Primeiro, as pessoas programadoras faziam seus programas em cartões perfurados, isso em 1800, la na industria têxtil. Cada um dos furos dizia para os teares programáveis onde eles deveriam fazer os pontos de costura, os cartões eram lidos e interpretados pelo tear.

<img src="https://www.stylourbano.com.br/wp-content/uploads/2017/02/TEAR-JACQUARD-min.jpg" alt="Cartões perfurados na industria têxtil" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />>
<br />

Deste princípio, em 1840, Charles Babbage propos o primeiro computador mecânico capaz de ler cartões perfurados e realizar calculos matemáticos. Ele nunca foi construído devido a complexidade necessária e os elevados custos. Sua ideia serviu de base para que em 1842, Ada Lovelace escrevesse o primeiro algoritmo de compuutador, que poderia ser executado neste computador mecânico.

<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Babbages_Analytical_Engine%2C_1834-1871._%289660574685%29.jpg" alt="Computador mecânico de Babbage"style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />
<br />

Ok, mas chega de história, falei tudo isso para dizer que nos cartões perfurados, tinhamos código binário de máquina. Eles eram lidos por esses dispositivos e interpretados por seus processadores. Em 1906, Herman Hollerith construi a empresa que se tornaria a IBM depois. Isso é relevante, pois ele construiu computadores que liam cartões perfurados e executavam diferentes programas, dependendo do conteúdo dos cartões lidos. Isso permitia que o mesmo dispositivo fosse utilizado para realizar diferentes tarefas, sem a necessidade de reconstruir o dispositivo.

<img src="https://i.ytimg.com/vi/17On5ItcrBA/maxresdefault.jpg" alt="Máquina de Herman Hollerith"style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }} />
<br />



:::tip[Como os programas são interpretados pelo computador]

<iframe width="560" height="315" src="https://www.youtube.com/embed/QXjU9qTsYCc?si=sJ8t1jfRnkC2t27h" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::


## x. Referencias

<iframe width="560" height="315" src="https://www.youtube.com/embed/EFmxPMdBqmU?si=7Ry1bfAdNR7GDDh1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>