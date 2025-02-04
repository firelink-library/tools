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

O terminal vive em um interstício interessante no imaginário coletivo dos
programadores. Para uns, é o seu fiel escudeiro. Um Sancho Pança virtual,
responsável por carregar todas as suas importantes ferramentas para o combate
de moinhos de vento. Para estes programadores, o contraste da tela preta com
letras brancas tem um ar de familiaridade tal qual um bolo de fubá servido em
um prato de vidro na cozinha da sua avó. 

Há, no entanto, um segundo grupo e é aí que mora uma dicotomia interessante.
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
fonte não são particularmente interessantes para esta discussão, portanto vamos
manter algum semblante de pragmatismo ao mencionar apenas a forma como se opera
o *ENIAC*: havia, nele, painéis com contatos elétricos e cabos conectores. Cada
padrão de energização destes contatos representava um valor numérico em escala
binária. Haviam, também, lâmpadas que serviam como a saída numérica do
computador. O princípio da computação exigia um trabalho braçal executado quase
exclusivamente por mulheres, conhecidas como *computadoras*.

Como uma curiosidade, o nome *computadoras* também é uma herança da segunda
guerra. Na ausência de máquinas que automatizassem os cálculos aritméticos
necessários para decriptação dos códigos alemãos, o único substituto possível
era utilizar mão de obra com qualificação em matemática básica. Essa mão de
obra era quase exclusivamente composta por mulheres. Não se deve, no entanto,
imputar qualquer senso de equidade nas intenções por trás dessa preferência;
ocorre que era socialmente aceitável que mulheres recebessem muito menos do que
homens para desempenhar essa função.

Segue assim, então, a utilização dos primeiros computadores eletrônicos da
história. Trocam-se os cabos e conectores pelos botões, trocam-se as lâmpadas
pelas telas, mas o princípio de funcionamento é o mesmo: exige operadores e não
executa mais de um programa por vez.

Pulando quase vinte anos mais tarde, quando já se apresentava o computador como
uma ferramenta mais padronizada - e, de modo geral, mais útil -, quando já
havia se estabelecido o paradigma do computador como um *mainframe* e já havia
se estabelecido *sistemas operacionais* como o *Unix*. Nesse momento já não é
mais aceitável a restrição de um usuário por vez e um processo por vez. A
resposta para esse problema é a criação de sistemas operacionais *multitarefa*.
Em particular, foi importante a criação do **Multics**.

Com um computador multitarefa, já não é mais razoável seguir o modelo das
*computadoras* de operação. Surgem, então, os **teleterminais**. Tratam-se de
*telas burras*, ou seja, sem capacidade computacional em si, mas que conseguem
se conectar com *mainframes* para enviar comandos e receber as respostas desses
comandos. Surge, enfim, o esqueleto que até hoje fundamenta o **terminal**.

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

Décadas depois, o paradigma da computação pessoal garante que já não se usa
mais *teleterminais* ou *teletypewriters*, mas a sua influência ainda é sentida
através dos **emuladores de terminal**. Os emuladores de terminal são programas
com uma interface de usuário simples, baseadas apenas em texto puro, que servem
exatamente o mesmo propósito que antes era incumbido aos teleterminais. 

Os emuladores de terminal variam em funcionalidade desde os mais simples - que
se limitam apenas a recriar a experiência dos teleterminais - até os mais
modernos, com suporte à GPU, multiplas *tabs* e até mesmo *ia* generativa.

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
Se não, eu mesmo acabo com a farsa; esse artigo é tanto sobre o terminal
quanto sobre a confusão que as pessoas fazem com os termos que permeiam o plano
dos terminais. A primeira confusão já deve ter sido desvendada adequadamente: o
**emulador de terminal** é apenas o programa que cria a interface entre o
usuário e os comandos que expõem as ferramentas de sistema. Vamos para a
segunda: **BASH** é uma *linguagem*, não o terminal em si.

Para entender essa distinção, basta considerar novamente o princípio da
computação. Imagine que, para cada novo fabricante de *mainframe*, surgia
também uma série de comandos distintos. Em outras palavras, o profissional
responsável por interagir com os primeiros computadores precisava aprender
novos comandos toda vez que trocava-se o fabricante. 

Não é difícil inferir que, logo que os sussuros do ENIAC ameaçaram se tornar
ventos circumnavegantes, houve uma pressão para criar um *padrão* para esses
comandos. Eis que surge o padrão **RUNCOM** - de *Run Commands* -, que teve em
sua imagem a criação do **Shell**, do sistema **Unix**. Uma curiosidade sobre o
*RUNCOM* é a herança que pode ser vista até hoje em sistemas com base *Unix*;
os arquivos de configuração terminados em *rc* (e.g. *bashrc*).

**BASH** é uma evolução do **Shell**. O acrônimo significa **Bourne Again
Shell**. Outras evoluções incluem o **ZSH - Zoomer Shell** ou o **FISH - sei
lá**. Segue abaixo um vídeo elaborando com mais detalhes as diferenças entre as
principais linguagens disponível para o terminal.

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

## 4. Comandos mais comuns

Para finalizar este artigo, resta apenas apresentar-lhes 
