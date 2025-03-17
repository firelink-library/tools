---
title: Python com HTMX
sidebar_position: 1
slug: /python-htmx
---


import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## 1. HTMX

O HTMX é uma biblioteca que permite que você construa aplicações web interativas sem escrever JavaScript. Ele é uma alternativa ao uso de JavaScript puro ou de frameworks como o React, Angular e Vue.

Vale destacar que ao utilizar HTMX, vamos ter uma aplicação que, idealmente, vai ser diferente de uma aplicação que utiliza REST como forma de troca de mensagens. Isso porque estaremos construindo uma aplicação que vai receber HTML e não JSON. Chamamos este tipo de aplicação de aplicação `HTML-first`, ou de Hypermidia.

Sugiro a leitura do artigo (Hypermedia-Driven Applications)[https://htmx.org/essays/hypermedia-driven-applications/], para compreender melhor os conceitos apresentados. Vale destacar do artigo:

> The Hypermedia Driven Application (HDA) architecture is a new/old approach to building web applications. It combines the simplicity & flexibility of traditional Multi-Page Applications (MPAs) with the better user experience of Single-Page Applications (SPAs).
>
>The HDA architecture achieves this goal by extending the existing HTML infrastructure of the web to allow hypermedia developers to create more powerful hypermedia-driven interactions.
>Following the REST notion of architectural constraints, two such constraints characterize the HDA architecture:
> - An HDA uses declarative, HTML-embedded syntax rather than imperative scripting to achieve better front-end interactivity
> - An HDA interacts with the server in terms of hypermedia (i.e. HTML) rather than a non-hypermedia format (e.g. JSON)
>
>By adopting these two constraints, the HDA architecture stays within the original REST-ful architecture of the web in a way that the SPA architecture does not.
>In particular, HDAs continue to use Hypermedia As The Engine of Application State (HATEOAS), whereas most SPAs abandon HATEOAS in favor of a client-side model and data (rather than hypermedia) APIs.

Agora vamos avaliar como construir algumas aplicações utilizando HTMX. Todas elas estão com seu código fonte disponível aqui na pasta `src` do nosso repositório do (Github)[https://github.com/Murilo-ZC/M5-Inteli-Eng-Comp].

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://unpkg.com/htmx.org@1.9.11" integrity="sha384-0gxUXCCR8yv9FM2b+U3FDbsKthCI66oH5IA9fHppQq9DDMHuMauqq1ZHBpJxQ0J0" crossorigin="anonymous"></script>
    <title>Testando o HTMX</title>
</head>
<body>
    <!-- O botão vai fazer uma requisição post para o servidor -->
    <button type="button" hx-post="http://localhost:8000/ola" hx-target="#respostaServidor">
        Ola Mundo
    </button>

    <div id="respostaServidor"></div>
</body>
</html>
```

Vamos compreender o que está acontecendo no código acima:

- `script src="https://unpkg.com/htmx.org@1.9.11"`: estamos importando a biblioteca do HTMX para o nosso projeto. A versão utilizada foi a mais recente disponível do projeto. Ela está disponível no CDN do unpkg.
- `hx-post="http://localhost:8000/ola"`: estamos definindo que ao clicar no botão, vamos fazer uma requisição POST para o servidor. O servidor que estamos utilizando é o `http://localhost:8000/ola`.
- `hx-target="#respostaServidor"`: estamos definindo que a resposta do servidor vai ser inserida no elemento com o id `respostaServidor`.
- `div id="respostaServidor"`: é o elemento que vai receber a resposta do servidor.

Agora vamos configurar o servidor para receber a requisição do cliente. Para isso, vamos utilizar o Flask. 

## 2. Servidor Flask de Hypermidia

Vamos criar um servidor Flask que vai receber a requisição do cliente e vai retornar uma resposta em HTML. Para isso, vamos criar um ambiente virtual e instalar as dependências necessárias.

```bash
# Criar o ambiente virtual
python3 -m venv venv
# Ativar o ambiente virtual
source venv/bin/activate
# Instalar as dependências
pip install -r requirements.txt
```

Agora vamos avaliar o código fonte que vai fazer nosso sistema funcionar:

```python
# Aplicação de servidor HTTP Flask que retonar HTML
from flask import Flask, request
from flask_cors import CORS
from random import randint
import time

app = Flask(__name__)

# Habilitar o CORS para todos os domínios
CORS(app)

@app.route('/')
def index():
    return '<h1>Olá, mundo!</h1>'

@app.route('/ola', methods=['POST'])
def ola():
    return '<div><h2>Olá, mundo Diferente!</h2></div>'

@app.route('/numero', methods=['GET'])
def sortea_numero()->int:
    return f'<div>Número Sorteado: {str(randint(1, 100))}</div>'

@app.route('/hora-delay', methods=['GET'])
def devolve_hora_com_delay():
    time.sleep(5)
    return f'<div>Hora: {time.strftime("%H:%M:%S")}</div>'

# Rota para receber dados enviados via POST
@app.route('/recebe-dados', methods=['POST'])
def recebe_dados():
    email = request.form['email']
    nome = request.form['nome']
    return f'<div>Nome: {nome} - Email: {email}</div>'

# Rota para receber dados enviados via POST - dados enviados como JSON
@app.route('/recebe-dados-json', methods=['POST'])
def recebe_dados_json():
    dados = request.get_json()
    email = dados['email']
    nome = dados['nome']
    return f'<div>Nome: {nome} - Email: {email}</div>'

#Rota para receber um arquivo enviado por multipart/form-data
@app.route('/recebe-arquivo', methods=['POST'])
def recebe_arquivo():
    print(request.files)
    arquivo = request.files['arquivo']
    arquivo.save(arquivo.filename)
    return f'<div>Arquivo {arquivo.filename} recebido com sucesso!</div>'

if __name__ == '__main__':
    app.run(debug=False, host='0.0.0.0', port=8000)
```

Essa aplicação é longa, vamos avaliar o que ela está fazendo:

- `CORS(app)`: estamos habilitando o CORS para todos os domínios. Isso é necessário para que o cliente consiga fazer requisições para o servidor.
- `@app.route('/')`: estamos definindo uma rota que vai retornar um HTML com a mensagem `Olá, mundo!`.
- `@app.route('/ola', methods=['POST'])`: estamos definindo uma rota que vai retornar um HTML com a mensagem `Olá, mundo Diferente!`. Essa rota só vai ser acessível por requisições POST.
- `@app.route('/numero', methods=['GET'])`: estamos definindo uma rota que vai retornar um HTML com um número sorteado entre 1 e 100. Essa rota só vai ser acessível por requisições GET.
- `@app.route('/hora-delay', methods=['GET'])`: estamos definindo uma rota que vai retornar um HTML com a hora atual. Essa rota só vai ser acessível por requisições GET. Ela tem um delay de 5 segundos.
- `@app.route('/recebe-dados', methods=['POST'])`: estamos definindo uma rota que vai receber um formulário com os campos `email` e `nome`. Essa rota só vai ser acessível por requisições POST.
- `@app.route('/recebe-dados-json', methods=['POST'])`: estamos definindo uma rota que vai receber um JSON com os campos `email` e `nome`. Essa rota só vai ser acessível por requisições POST.
- `@app.route('/recebe-arquivo', methods=['POST'])`: estamos definindo uma rota que vai receber um arquivo enviado por `multipart/form-data`. Essa rota só vai ser acessível por requisições POST.


:::tip[CORS]

O CORS é um mecanismo de segurança implementado pelos navegadores da web para proteger os usuários contra ataques de origem cruzada. Ele controla as solicitações HTTP feitas por scripts em uma página da web para recursos localizados em um domínio diferente do domínio da própria página.

A importância do CORS reside na necessidade de garantir que as solicitações feitas por scripts em uma página da web sejam restritas a recursos apenas de origens confiáveis. Isso ajuda a prevenir ataques maliciosos, como ataques de roubo de sessão, que podem ocorrer quando um script em uma página maliciosa tenta fazer solicitações não autorizadas para recursos em outro domínio.

Ao configurar as políticas CORS em um servidor web, você pode especificar quais origens estão autorizadas a acessar os recursos do servidor. Isso permite que os desenvolvedores controlem de forma granular quais recursos podem ser acessados por quais origens, ajudando a garantir a segurança e a integridade dos dados de uma aplicação web.

<iframe width="560" height="315" src="https://www.youtube.com/embed/GZV-FUdeVwE?si=QS6dIaWe06uXo2ws" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/4KHiSt0oLJ0?si=gKHD3wiB_ZvturrM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/PNtFSVU-YTI?si=UOdfwwBleTDnhWl1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/vWl5XcvQBx0?si=RYBhx8xZYtS3Te-_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

:::

Agora nossa aplicação vai conseguir realizar a requisição para o servidor. Vamos agora avaliar algumas outras requisições que podemos fazer utilizando o HTMX em nossa aplicação. Pessoal, lembrando que mais detalhes sobre a utilização do HTMX deve ser consultado na documentação oficial do projeto (HTMX)[https://htmx.org/].

## 3. Estudando o HTMX

### 3.1. Configurando Eventos e Funções com o HTMX

Vamos avaliar o código a seguir:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://unpkg.com/htmx.org@1.9.11" integrity="sha384-0gxUXCCR8yv9FM2b+U3FDbsKthCI66oH5IA9fHppQq9DDMHuMauqq1ZHBpJxQ0J0" crossorigin="anonymous"></script>
    <title>Eventos Especiais</title>
</head>
<body>
    <!-- Este evento especial é acionado quando a página é carregada -->
    <!-- O trigger "load" é carregado quando a página é carrega. Ele não depende da interação do usuário com a página -->
    <div hx-get="http://localhost:8000/" 
         hx-target="#respostaLoadPagina"
         hx-trigger="load">
        Evento de Página sendo Carregada, na Div aqui de baixo!
    </div>

    <div id="respostaLoadPagina"> Resposta da Página Carrega</div>

    <!-- Evento disparado quando um elemento é apresentado no viewport -->
    <div hx-get="http://localhost:8000/" 
         hx-trigger="revealed"
         style="margin-top: 1400px;">
        Carregado quando aparece inteiro
    </div>

    <!-- É possível também configurar o disparo evento para apenas uma porção pequena do elemento já estiver visível na tela -->
    <!-- A porcentagem que deve estar vísivel na tela para realizar a requisição vai variar de acordo com o valor definido no atributo threshold. Por padrão é 0.0, na primeira aparição parcial ele já realiza a requisição. -->
    <div hx-get="http://localhost:8000/" 
         hx-trigger="intersect threshold:0.2"
         style="margin-top: 1400px;">
        Carregado quando aparece uma parte
    </div>
</body>
</html>
```

Vamos avaliar o que está acontecendo no código acima:

- `hx-trigger="load"`: estamos definindo que a requisição vai ser feita quando a página for carregada. Isso é um evento especial que não depende da interação do usuário com a página.
- `hx-trigger="revealed"`: estamos definindo que a requisição vai ser feita quando o elemento for apresentado no viewport. Isso é um evento especial que depende da interação do usuário com a página.
- `hx-trigger="intersect threshold:0.2"`: estamos definindo que a requisição vai ser feita quando uma porção do elemento for apresentado no viewport. Isso é um evento especial que depende da interação do usuário com a página. O valor `0.2` indica que 20% do elemento deve estar visível para que a requisição seja feita.

### 3.2. Configurando Requisições com o HTMX

Agora vamos avaliar o seguinte código fonte:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://unpkg.com/htmx.org@1.9.11" integrity="sha384-0gxUXCCR8yv9FM2b+U3FDbsKthCI66oH5IA9fHppQq9DDMHuMauqq1ZHBpJxQ0J0" crossorigin="anonymous"></script>
    <title>Requisições HTTP</title>
</head>
<body>
    <!-- O comportamento default é realizar requisições quando um elemento for clicado -->
    <button type="button" hx-get="http://localhost:8000/">
        Fazendo Requisição GET
    </button>

    <!-- Configurando o atributo hx-trigger, é possível determinar o evento que será ouvido. São os mesmos de JS em lowercase. -->
    <!-- CUIDADO: Desta forma, diversas requisição serão realizadas quando o mouse entrar na região da div -->
    <div hx-get="http://localhost:8000/" hx-trigger="mouseenter">
        Realizando a requisição quando o mouse entrar!
    </div>

    <!-- Podemos aplicar modificadores no trigger de um elemento -->
    <!-- Os modificadores de trigger auxiliam no controle do evento, alterando seu comportamento -->
    <!-- O modificador once faz com que a requisição seja realizada apenas uma vez -->
    <!-- Mesmo que o evento ocorra novamente, ele não vai ser lançado novamente -->
    <div hx-get="http://localhost:8000/" hx-trigger="mouseenter once">
        Modificador de Trigger
    </div>

    <!-- Modifica o evento de mudança de um input -->
    <input type="text" hx-get="http://localhost:8000/" hx-trigger="change delay:3s">

    <!-- O Delay pode ser utilizado em outros elementos também -->
    <div hx-get="http://localhost:8000/" hx-trigger="click delay:3s from:#requestTrigger">Teste com delay</div>

    <!-- É possível configurar outro elemento para realizar o disparo de um trigger -->
    <!-- Por exemplo, o botão a seguir dispara o request do elemento anterior -->
    <!-- Para esse comportamento utilizando o modificador from do HTMX -->
    <button type="button" id="requestTrigger">
        Disparar requisição de outro elemento na página
    </button>
    
</body>
</html>
```

Vamos avaliar o código anterior:

- `hx-trigger="mouseenter"`: estamos definindo que a requisição vai ser feita quando o mouse entrar na região da div. Isso é um evento especial que depende da interação do usuário com a página.
- `hx-trigger="mouseenter once"`: estamos definindo que a requisição vai ser feita quando o mouse entrar na região da div. Isso é um evento especial que depende da interação do usuário com a página. O modificador `once` faz com que a requisição seja realizada apenas uma vez.
- `hx-trigger="change delay:3s"`: estamos definindo que a requisição vai ser feita quando o valor do input for alterado. Isso é um evento especial que depende da interação do usuário com a página. O modificador `delay:3s` faz com que a requisição seja realizada após 3 segundos.
- `hx-trigger="click delay:3s from:#requestTrigger"`: estamos definindo que a requisição vai ser feita quando o elemento for clicado. Isso é um evento especial que depende da interação do usuário com a página. O modificador `delay:3s` faz com que a requisição seja realizada após 3 segundos. O modificador `from:#requestTrigger` faz com que o evento seja disparado pelo elemento com o id `requestTrigger`.

### 3.3. Indicador de Progresso

Vamos avaliar o código a seguir:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Indicador de Progresso</title>
    <script src="https://unpkg.com/htmx.org@1.9.11" integrity="sha384-0gxUXCCR8yv9FM2b+U3FDbsKthCI66oH5IA9fHppQq9DDMHuMauqq1ZHBpJxQ0J0" crossorigin="anonymous"></script>
</head>
<body>
    <!-- O indicador de progresso pode ser adicionado a diversas ações. -->
    <!-- Basta adicionar a classe "htmx-indicator" no elemento que deve ser exibido enquanto a ação estiver ocorrendo -->
    <!-- O indicador de progresso é exibido enquanto a requisição estiver sendo realizada -->
    <!-- IMPORTANTE: Essa implementação faz com que o mostrador apenas seja exibido uma vez, depois ele vai ser removido do DOM. -->
    <div hx-get="http://localhost:8000/hora-delay"
         hx-trigger="click">
        Indicador de progresso!
        <p class="htmx-indicator">
            Recebendo dados...
        </p>
    </div>

    <!-- O indicador de progresso pode ser adicionado a diversas ações. -->
    <!-- Devemos definir o hx-indicator do elemento que vai ser carregado enquanto a ação estiver acontecendo -->
    <div hx-get="http://localhost:8000/hora-delay"
         hx-trigger="click"
         hx-indicator="#loading-element">
        Indicador de Progresso Com Implementação Externa!
    </div>
    <p id="loading-element" class="htmx-indicator">
        Carregando...
    </p>
</body>
</html>
```

Vamos avaliar o código anterior:

- `class="htmx-indicator"`: estamos definindo que o elemento vai ser exibido enquanto a requisição estiver sendo realizada. Isso é um indicador de progresso que depende da interação do usuário com a página.
- `hx-indicator="#loading-element"`: estamos definindo que o elemento com o id `loading-element` vai ser exibido enquanto a requisição estiver sendo realizada. Isso é um indicador de progresso que depende da interação do usuário com a página.

### 3.4. Configurando Polling de Dados com o HTMX

O objetivo deste código é trabalhar com o evento de `polling` de dados. Vamos avaliar o código a seguir:

- TODO


## 4. Material de Referência


<Tabs>
  <TabItem value="autoestudos-obrigatorios" label="📘 Autoestudos Obrigatórios" default>
     
    <details> 
        <summary mdxType="summary"> How to Create an Instant Search Bar With Flask and HTMX</summary>

        - https://www.youtube.com/watch?v=PWEl1ysbPAY
    </details> 
    
    <details> 
        <summary mdxType="summary"> HTMX - Clean, Dynamic HTML Pages - Talk Python to Me Ep.321</summary>

        - https://www.youtube.com/watch?v=4wjqsPtj2QY
    </details> 

  </TabItem>
  <TabItem value="autoestudos-adicionais" label="📓 Autoestudos Adicionais">
    
    <details> 
        <summary mdxType="summary">	FULL Introduction To HTMX Using Golang</summary>
        Foquem na etapa da HTMX, não no Golang. Ele pode ser substituído pelo Flask.
        - https://www.youtube.com/watch?v=x7v6SNIgJpE
    </details> 
    <details> 
        <summary mdxType="summary">	htmx in 100 seconds</summary>
        - https://www.youtube.com/watch?v=r-GSGH2RxJs
    </details> 
    <details> 
        <summary mdxType="summary">	HTMX for Impatient Devs</summary>
        - https://www.youtube.com/watch?v=TT7SV-bAZyA
    </details> 
    <details> 
        <summary mdxType="summary">	HTMX Crash Course | Dynamic Pages Without Writing Any JavaScript</summary>
        - https://www.youtube.com/watch?v=0UvA7zvwsmg
    </details> 
    <details> 
        <summary mdxType="summary">	The Most Important Lesson From HTMX</summary>
        - https://www.youtube.com/watch?v=f2wYvIVWR6M
    </details> 

  </TabItem>
</Tabs>



:::tip[Material de Apoio]

Pessoal aqui vou deixar algum material de apoio que eu recomendo ***FORTEMENTE*** que vocês leiam, em especial se vocês tiverem alguma dificuldade com o conteúdo de HTML e CSS.

<details> 
    <summary mdxType="summary">	HTML and CSS for Python Developers</summary>
        - https://realpython.com/html-css-python/
</details> 
<details> 
    <summary mdxType="summary">	Getting started with CSS</summary>
        - https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/Getting_started
</details> 
<details> 
    <summary mdxType="summary">	Learn CSS in 5 minutes - A tutorial for beginners</summary>
        - https://www.freecodecamp.org/news/get-started-with-css-in-5-minutes-e0804813fc3e/
</details> 
<details> 
    <summary mdxType="summary">	Bulma: the modern CSS framework that just works.</summary>
        - https://bulma.io
</details> 
<details> 
    <summary mdxType="summary">	Bulma CSS Framework - complete tutorial</summary>
        - https://www.youtube.com/watch?v=LBzZLzu2GKo
</details> 

Pessoal esse vídeo aqui é bem longo, mas ele traz uma abordagem bem interessante desde o Figma, implementação do HTML e o desenvolvimento do CSS 💻.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Lx_YsoMgP40?si=0DblQixY7pvYPOsm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

:::