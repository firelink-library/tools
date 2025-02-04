---
title: O terminal
sidebar_position: 2
slug: /command-line-interface
---

import ArchBtw from '@site/static/img/arch_btw.png'
import EniacPannel from '@site/static/img/eniac_pannel.png'
import TeleTerminal from '@site/static/img/canon_teleterminal.png'

# O terminal

<img 
  src={ArchBtw}
  alt="I use Arch, BTW"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>

O terminal vive em um interstício curioso no imaginário coletivo dos
programadores. Para uns, é o seu fiel escudeiro. Um Sancho Pança virtual,
responsável por carregar todas as suas importantes ferramentas para o combate
de moinhos de vento. Para estes programadores, o contraste da tela preta com
letras brancas tem um ar de familiaridade tal qual um bolo de fubá servido em
um prato de vidro na cozinha da avó. 

Há, no entanto, um segundo grupo e é aí que mora uma divergência curiosa.
Para este grupo, abrir o terminal é como ser convidado para um restaurante
francês e não compreender o motivo da sequência de talheres - aparentemente
redundantes - dispostos à mesa. Nessa situação é perfeitamente compreensível
que desenvolva-se, no freguês faminto, um certo ressentimento com relação
àquilo que - para ele - só pode ser compreendido como uma futilidade elitista.

Essa divisão, no entanto, não é inata do indivíduo. Assim como é possível a
metamorfose de um colega que olha desconfiado para um prato de atum cru fatiado
em um entusiasta da culinária japonesa, é também possível que o ressentimento
que alguns desenvolvedores sentem com a aparente complexidade do terminal vire
uma sensação de familiaridade. Entenda, portanto, este breve artigo como um
convite; uma porta que se abre para que o *bistrô* vire a cozinha da avó.

Antes de cortarmos o bolo, faço mais um apelo para aqueles que não se convencem
que a beleza do processo justifica a espera necessária para que uma lagarta
vire borboleta. Segue então um argumento mais utilitário: o terminal é um
ambiente estável e praticamente onipresente no mundo dos servidores. Sendo
assim, tem tanto mais valor alguém que consegue navegar por telas
monocromáticas do que quem só convive bem com cores saturadas.

## 1. Um pouco de história

Tendo apresentado o tema e objetivo deste artigo, vamos conversar um pouco
sobre hist́ória.

Vamos viajar para o ano de 1943, visitando um mundo em reconstrução após a
segunda grande guerra. Entre as vigas distorcidas e sob a ameaça de novos
tempos austeros para milhões de pessoas, os ventos atlânticos da Pensilvânia
sussurram a revolução da comunicação humana. Nasce o primeiro computador e
integrador numérico eletrônico, ou *ENIAC*.

<img 
  src={EniacPannel}
  alt="Painél operacional do Eniac"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>
<center><p>Figura - O painel do ENIAC sendo operado pelas *computadoras*</p></center>

Os princípios de funcionamento do *ENIAC* e dos computadores que bebem da sua
fonte não são particularmente interessantes para esta discussão, portanto
podemos ignorá-los por enquanto. Foquemos, então, na forma como se opera o
*ENIAC*: operadores interagiam com painéis com contatos elétricos e cabos
conectores. Cada padrão de energização destes contatos representava um valor
numérico em escala binária. Havia, também, lâmpadas que serviam como a saída
numérica do computador. O princípio da computação exigia um trabalho braçal
executado quase exclusivamente por mulheres, conhecidas como *computadoras*.

Como uma curiosidade, o nome *computadoras* também é uma herança da segunda
guerra. Na ausência de máquinas que automatizassem os cálculos aritméticos
necessários para decriptação dos códigos nazistas, o único substituto
disponível era a mão de obra qualificada em matemática básica. Essa mão de
obra era quase exclusivamente composta por mulheres. Não se deve, no entanto,
imputar qualquer senso de equidade ou diversidade nas intenções por trás dessa
preferência; ocorre que era socialmente aceitável que mulheres recebessem muito
menos do que homens para desempenhar essa função. Com o surgimento dos
computadores eletrônicos, as *computadoras* largaram as canetas e pegaram, em
seu lugar, os cabos e contatores.

Segue assim, então, a utilização dos primeiros computadores eletrônicos da
história. Trocam-se os cabos e conectores pelos botões, trocam-se as lâmpadas
pelas telas, mas o princípio de funcionamento é o mesmo: exige operadores e não
executa mais de um programa por vez.

Pulando quase vinte anos mais tarde, quando a promessa do computador já se
mostrava mais madura; quando já se tinha estabelecido como dominante a figura
do sistema operacional para promover padronização; quando já era comum e útil
lançar mão de um *mainframe* para atividades computacionais de pesquisa ou
empresariais; foi nesse momento que a limitação de um programa e um
operador por vez se tornou o gargalo do processo. A solução veio na forma de
sistemas operacionais *multitarefa*. Em particular, destaca-se o **Multics**
como o principal precursor dessa mudança.

Com um computador multitarefa, foi possível aposentar as mãos das computadoras
e trocá-las pelos **teleterminais**. Tratam-se de *telas burras*, ou seja, sem
capacidade computacional em si, mas que conseguem se conectar com *mainframes*
para enviar comandos e receber as respostas desses comandos. Surge, enfim, o
esqueleto que até hoje fundamenta o **terminal**.

<img 
  src={TeleTerminal}
  alt="Tele terminal da Canon"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>
<br/>
<center><p>Figura - Teleterminal da Canon, AP500. Uma curiosidade sobre este
tipo de teleterminal que não utiliza telas, mas máquinas de escrever, é o seu
nome; teletypewriter, ou **TTY**.</p></center>

## 2. Emuladores de terminal

Décadas depois, o paradigma da computação pessoal tornou obsoletos os
*teleterminais* e *teletypewriters*, mas não se pode apagar a influência de
ferramentas utilizadas e otimizadas por anos. Segue, assim, que até hoje
enxergamos o fantasma do terminal em nosso computadores e servidores. A esse
fantasma damos o nome **emulador de terminal**.

Os emuladores de terminal são programas com uma interface de usuário simples,
baseadas apenas em texto puro, que servem exatamente o mesmo propósito que
antes era incumbido aos teleterminais. A diferença é que eles existem dentro de
ambientes de interface de usuário gráficas - *GUI* - e já não são as máquinas
burras do passado.

Os emuladores de terminal variam em funcionalidade desde os mais simples - que
se limitam apenas a recriar a experiência dos teleterminais - até os mais
modernos, com suporte à GPU, multiplas abas e até mesmo *ia* generativa
(usuários de Mac - ver *Warp*).

O vídeo abaixo é um presente e uma sugestão para você. Sim você! Que mesmo já
dominando o básico sobre o terminal quis ler o que eu tinha a dizer sobre o
assunto. Espero que tenha aprendido algo de novo. Olha esse emulador de
terminal, lançado no fechar das cortinas de 2024:

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/3wq0RFYAvNo" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

## 3. As linguagens do terminal

A essa altura talvez você já tenha desvendado um objetivo secreto deste artigo.
Se não, eu mesmo acabo com a farsa: este artigo é tanto sobre o terminal
quanto sobre a confusão que as pessoas fazem com os termos que permeiam o plano
dos terminais. A primeira confusão já deve ter sido desvendada adequadamente; o
**emulador de terminal** é apenas o programa que cria a interface entre o
usuário e os comandos que expõem as ferramentas de sistema. Vamos para a
segunda: **BASH** é uma *linguagem*, não o terminal em si.

Para entender essa distinção, basta considerar novamente o princípio da
computação. Imagine que, para cada novo fabricante de *mainframe*, surgia
também uma série de comandos distintos. Em outras palavras, o profissional
responsável por interagir com os primeiros computadores precisava aprender
novos comandos toda vez que trocava-se o fabricante.

Não é difícil imaginar que, logo que os sussuros do ENIAC ameaçaram se tornar
ventos circumnavegantes, houve uma pressão para criar um *padrão* para esses
comandos. Eis que surge o padrão **RUNCOM** - de *Run Commands* -, que teve em
sua imagem a criação do **Shell**, do sistema **Unix**. Uma curiosidade sobre o
*RUNCOM* é a herança que pode ser vista até hoje em sistemas com base *Unix*;
os arquivos de configuração terminados em *rc* (e.g. *bashrc*).

A linguagem **Shell** é uma linguagem de programação como tantas outras que
você deve conhecer. Tem funcionalidades como laços de repetição, estruturas
condicionais, subrotinas, variáveis, arrays, entre outros. Também em comum com
algumas das linguagens mais utilizadas no mundo nos tempos atuais, *Shell* é
uma linguagem interpretada e não compilada. Sendo assim, diz-se que um programa
em *Shell* é um *script*.

**BASH** é uma evolução do **Shell**. O acrônimo significa **Bourne Again
Shell**. Outras evoluções incluem o **ZSH - Zoomer Shell** ou o **FISH - sei
lá**. Segue abaixo um vídeo elaborando com mais detalhes as diferenças entre as
principais linguagens disponíveis para o terminal.

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/dRdGq8khTJc" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

Aqui reitero novamente minha gratidão à você que já domina esse conteúdo, mas
mesmo assim me acompanhou durante as mais recentes elocubrações. Segue aqui uma
linguagem novinha em folha com um conceito bem interessante: o **Nushell**.

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/GPqV6rLfKR4" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

## 4. O prompt

Se o terminal/emulador de terminal é uma maneira de acessar o *hardware* do
computador e o *shell*/*bash*/*zsh* é a linguagem utilizada no terminal, resta
apenas abordarmos mais um conceito que comumente confunde-se em explicações
sobre o terminal: o **prompt**.

O *prompt* nada mais é do que a indicação para o usuário de que ele pode enviar
comandos à máquina. Sim. Simples assim. Para que esta seção não fique
dolorosamente rasa de conteúdo, segue aqui uma indicação de um prompt
configurável, para que você tenha um pouco mais do que só o caractere `>`. O
nome dele é *Starship*. Veja no vídeo abaixo o que pode ser feito utilizando
essa ferramenta (feita em *Rust*, para a felicidade dos amantes de crustáceos).

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/G7aWxK4395Y" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>


## 5. Os comandos

Para finalizar este artigo, resta apenas apresentar-lhes os comandos mais
comuns utilizados no terminal. Aqui, vamos seguir com os comandos necessários
para que você consiga se locomover e fazer o mínimo necessário. Para isso,
vamos abordar os seguintes comandos:

* ls
* cd
* cat
* touch
* rm
* rmdir
* mkdir
* man
* tldr

Antes de seguir com as explicações dos comandos, cabe uma palavrinha sobre o
que é conhecido como a *filosofia Unix*. **Unix**, como já estabelecemos, foi
um sistema operacional da era dos *mainframes* cuja influência é sentida até
hoje fortemente nos sistemas operacionais modernos. 

A maior parte dessa influência pode ser explicada pelo domínio de mercado do
*Unix* à época, que fez com que entusiastas buscassem soluções similares, mas
de fonte aberta e gratuita. Entre esses entusiastas, destaca-se *Linus
Torvalds*, que desenvolveu sua própria versão do *Unix* - *Linus' Unix*, ou
*Linux* -. De todo modo, a filosofia *Unix* no que tange programas que operam
no terminal é até hoje o padrão para sistemas operacionais.

No que consiste essa filosofia? É bem simples e pode ser resumida em duas
frases adequadamente: 

1. Todas as interfaces entre aplicações no terminal devem ser baseadas em
   texto; e
2. As aplicações do terminal devem se ocupar de apenas uma tarefa e fazê-la com
   eficácia e simplicidade.

Sobre a primeira parte, segue que a entrada e saída de qualquer programa
executado no terminal é composta apenas de texto. Se para você isso soa como
uma limitação, considere assistir o vídeo abaixo:

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/WgV6M1LyfNY" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

A segunda parte é uma imposição mais conceitual e pode ser explicada com um
exemplo: imagine que você queira 
