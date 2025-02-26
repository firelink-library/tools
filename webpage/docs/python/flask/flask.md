---
title: Flask
sidebar_position: 1
slug: /flask
---

## 1. Frame o que?

Pessoal ao longo deste encontro vamos compreender alguns conceitos importantes para o desenvolvimento dos nossos projetos: como construir soluções que possam ser acessadas via web, como criar um servidor e como acessar a aplicação web. Para isso, vamos passar por alguns conceitos fundamentais para depois iniciarmos a construção da nossa aplicação web, utilizando o microframework Flask.

Beleza, mas ainda não respondemos a pergunta: Framework? O que é isso?

> Murilão mas quem perguntou isso?

Vamos por partes, o conceito surge porque se formos buscar a informação sobre o que é o Flask de Python, vamos nos deparar com a seguinte informação:

> "*Flask is a lightweight WSGI web application framework. It is designed to make getting started quick and easy, with the ability to scale up to complex applications.*"

O que podemos tirar daqui que é importante para nós:
- O Flask é um conjunto de ferramentas para desenvolver aplicações Web;
- Existem algumas definições que colocam o Flask como um microframework. O Flask é considerado um microframework porque ele é minimalista e fornece apenas o essencial para o desenvolvimento de aplicações web, sem impor uma estrutura rígida ou incluir muitas funcionalidades prontas. Essa abordagem contrasta com frameworks mais completos, como o Django (também em Python), que são considerados full-stack frameworks (ou frameworks completos). 
- O Flask é altamente extensível. Em vez de incluir tudo "de fábrica", ele permite que você adicione funcionalidades conforme necessário, usando extensões ou bibliotecas de terceiros. 

## 2. Antes ainda, alguns conceitos fundamentais

Antes de qualquer outro avanço, vamos fazer um nivelamento sobre aplicações web, o que são, o que comem, como vivem e como podemos construir uma. Primeiro precisamos entender quais são as partes de uma aplicação e sua importância.

Existem diversos tipos de aplicação Web, um dos tipos mais conhecidos são os websites, que são acessados por meio de um navegador. Outros tipos de aplicações web são as APIs, que são acessadas por meio de requisições HTTP e retornam dados em formato JSON ou XML. As aplicações Web são programas que podem ser acessados através de um navegador da web, como o Google Chrome, Mozilla Firefox ou Microsoft Edge. Elas são compostas por diversos elementos que trabalham juntos para fornecer uma experiência interativa ao usuário.

<img 
  src="https://www.appventurez.com/wp-content/uploads/2020/07/web-application-architecture-infographic.jpg"
  alt="Arquitetura de uma aplicação web simplificada"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>


Avaliando alguns destes elementos, podemos destacar:

- ***Cliente***: O navegador do usuário.
- ***Servidor***: O computador que armazena os arquivos da aplicação e processa os pedidos.
- ***HTTP***: O protocolo usado para comunicação entre o cliente e o servidor.
- ***HTML, CSS e JavaScript***: Linguagens usadas para desenvolver a interface da aplicação, a lógica da aplicação e a interatividade.
- ***Banco de dados***: Armazena informações sobre produtos, usuários, pedidos, para citar algumas aplicações.
- ***Interface do usuário***: Páginas da aplicação que o usuário visualiza, como a página inicial, a página de produtos e a página de checkout.
- ***Lógica da aplicação***: Código que define como a aplicação responde às ações do usuário, como adicionar um produto ao carrinho ou realizar um pedido.
- ***Camada de acesso a dados***: Código que interage com o banco de dados para armazenar, recuperar e atualizar informações sobre produtos, usuários e pedidos.

Diferentes aplicações podem ter diferentes arquiteturas, mas a maioria das aplicações web modernas segue uma arquitetura de três camadas, que divide a aplicação em três partes principais: a interface do usuário, a lógica da aplicação e a camada de acesso a dados. Um exemplo de aplicação mais completa pode ser vista na imagem abaixo. Uma explicação mais detalhada sobre a arquitetura de três camadas pode ser vista [aqui](https://www.aalpha.net/blog/web-application-architecture/).

<img 
  src="https://cdn-cjmik.nitrocdn.com/UjszoEMIGzQLBmRYICliaPmdTnvQlovN/assets/images/optimized/rev-22ebbc4/www.aalpha.net/wp-content/uploads/2023/01/Components-of-Web-Application-Architecture.webp"
  alt="Arquitetura de uma aplicação Web mais completa"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>


E um resumo sobre a aplicação pode ser vista em:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Sfzo4xm5eX8?si=OHnK6KcQ5OKR6UqP" title="How internet works in 4 minutes" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>


:::tip[Diferentes Arquiteturas]

Para conhecer mais sobre diferentes arquiteturas de aplicações:

<iframe width="560" height="315" src="https://www.youtube.com/embed/i53Gi_K3o7I?si=JHwYo3FC_G0gf903" title="20 System Design Concepts Explained" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

:::

Frente a esses conceitos, vamos entender como podemos construir uma aplicação web com Flask, um microframework para Python.


## 3. Python Flask

Para construir uma aplicação web, precisamos de um servidor que possa receber requisições e retornar respostas. O Flask é um microframework para Python que nos permite construir aplicações web de forma rápida e fácil. Ele é um dos frameworks mais populares para construção de aplicações web em Python, e é utilizado por empresas como Netflix, Reddit, Lyft, entre outras.

O Python em conjunto com nossa aplicação Flask é executada no servidor, que é um computador que armazena os arquivos da aplicação e processa os pedidos. O servidor é responsável por receber as requisições dos clientes, processar essas requisições e retornar respostas. O servidor é um programa que executa continuamente, aguardando por requisições e respondendo a elas.

O Flask é um microframework, o que significa que ele é um framework minimalista que fornece apenas o essencial para construir uma aplicação web, como falamos acima!! Ele é fácil de aprender e usar, e é uma ótima opção para construir aplicações web pequenas e médias. O Flask é extensível, o que significa que podemos adicionar funcionalidades adicionais através de extensões, que são pacotes de código que estendem as funcionalidades do Flask. Para conhecer mais sobre o Flask, acesse a [documentação oficial](https://flask.palletsprojects.com/en/latest/).

Para utilizarmos o Flask, vamos primeiro criar um ambiente virtual para nossa aplicação. Os arquivos de uma aplicação Flask são organizados de forma que possamos separar a lógica da aplicação em diferentes arquivos. Vamos instalar o Flask em nosso ambiente virtual:

```sh
# Cria o venv
python -m venv venv
# Ativa o venv - ambiente Windows
.\venv\Scripts\activate
# Agora, instala o Flask
python -m pip install flask
```

Agora vamos colocar um primeiro sistema para funcionar:

```py
# ola-flask.py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Ola Mundo!!</p>"
```

Agora podemos rodar nosso programa, para isso vamos utilizar o comando:

```sh
python -m flask --app ola-flask run
```

O que estamos fazendo aqui:
- Chamamos o Flask com o Python;
- Dizemos para o Flask onde está nosso programa principal.

O resultado:

```sh
 * Serving Flask app 'ola-flask'
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit
```

Ao acessar o endereço apresentado no terminal, vamos conseguir ver a imagem "Ola Mundo!!" no navegador. Com isso, conseguimos criar nossa primeira aplicação web com Flask.

:::danger[Atenção]

Até aqui pessoal, fizemos bastante coisa, mas vamos passar por cada um dos passos para compreender o que aconteceu. Se você está com dúvidas, não se preocupe, vamos passar por cada um dos passos para compreender o que aconteceu.

<img 
  src="https://media1.tenor.com/m/WgoifA87r5AAAAAC/mashle-mash-burnedead.gif"
  alt="Mashle Confused"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>

:::

Agora vamos compreender o que aconteceu aqui!

Primeiro, nosso arquivo fonte. O arquivo ola-flask.py é um arquivo Python que contém o código da nossa aplicação. Neste arquivo, importamos a classe Flask do módulo flask e criamos uma instância da classe Flask chamada app. A instância da classe Flask representa a nossa aplicação web. Em seguida, utilizamos o decorador @app.route("/") para associar a função hello_world com a rota /. O decorador @app.route("/") é uma forma de associar uma função com uma rota. Quando um cliente acessa a rota /, a função hello_world é executada e retorna a string "Ola Mundo!!".

O objeto app é um objeto especial nas aplicações Python. Ele é responsável por configurar a aplicação e gerenciar as requisições e respostas. O objeto app possui diversos métodos e atributos que nos permitem configurar a aplicação e adicionar funcionalidades adicionais. O método app.run() é utilizado para executar a aplicação. Ele inicia um servidor de desenvolvimento que aguarda por requisições e responde a elas. Outra características bastante importante é que o app de Flask é um singleton, ou seja, ele é único e compartilhado por toda a aplicação. Para conhecer mais sobre o padrão Singleton, acesse [aqui](https://refactoring.guru/pt-br/design-patterns/singleton).

Agora para executar nossa aplicação, utilizamos o comando `python -m flask --app ola-flask run`. O comando `python -m flask` é utilizado para executar o Flask. O argumento `--app ola-flask` é utilizado para especificar o nome do arquivo que contém a aplicação. O argumento `run` é utilizado para iniciar o servidor de desenvolvimento. O servidor de desenvolvimento é um servidor que aguarda por requisições e responde a elas. Ele é utilizado para testar a aplicação durante o desenvolvimento. O servidor de desenvolvimento é executado no endereço `http://127.0.0.1:5000`.

:::tip[Modo de Desenvolvimento]

Podemos alterar a porta onde o servidor de desenvolvimento é executado utilizando o argumento `--port`. Por exemplo, para executar o servidor de desenvolvimento na porta 8000, utilizamos o comando:

```sh
python -m flask --app ola-flask run --port 8000
```

Podemos também expor a aplicação para os outros elementos da rede, utilizando o argumento `--host`. Por exemplo, para expor a aplicação para os outros elementos da rede, utilizamos o comando:

```sh
python -m flask --app ola-flask run --host 0.0.0.0 --port 8000
```

:::

Quando nosso servidor recebeu a requisição, ele executou a função hello_world e retornou a string "Ola Mundo!!". O servidor de desenvolvimento é um servidor que aguarda por requisições e responde a elas.

:::danger[APENAS PARA DESENVOLVIMENTO]

Cuidado pessoal, o servidor de desenvolvimento é utilizado apenas para testar a aplicação durante o desenvolvimento. Ele não é adequado para uso em produção. Para implantar a aplicação em produção, utilizamos um servidor WSGI, como o Gunicorn ou o uWSGI. Para conhecer mais sobre o Gunicorn, acesse [aqui](https://gunicorn.org/).

Dizemos que uma aplicação vai para produção, quando ela está pronta para ser utilizada por usuários finais. A aplicação em produção é executada em um servidor de produção, que é um servidor que está configurado para executar a aplicação de forma segura e eficiente. O servidor de produção é utilizado para atender as requisições dos usuários finais e fornecer uma experiência interativa ao usuário.

:::

Agora vamos ajustar nossa aplicação para que ela se comporte como uma API, ou seja, que ela possa receber requisições e retornar respostas em formato padronizado.

## 4. Construção de uma API com Flask

Uma API Web, ou API RESTful, é um conjunto de definições e protocolos que permitem a comunicação entre diferentes sistemas através da web. Ela funciona como um intermediário, possibilitando que um sistema (cliente) solicite dados ou execute ações em outro sistema (servidor) de forma padronizada e segura.

1. `O cliente faz uma requisição`: O cliente envia uma requisição para a API, geralmente através do protocolo HTTP. A requisição especifica o método desejado (GET, POST, PUT, DELETE), o endpoint da API e os dados da requisição.
2. `A API processa a requisição`: A API recebe a requisição e a processa de acordo com o método especificado. Ela pode acessar um banco de dados, executar um script ou realizar qualquer outra operação necessária.
3. `A API retorna uma resposta`: A API retorna uma resposta para o cliente, geralmente em formato JSON ou XML. A resposta pode conter dados, mensagens de erro ou outros resultados da operação.

Agora vamos ajustar nossa aplicação para que ela se comporte como uma API. 

> Mas Murilão, eu não sei o que é uma API!

Calma! Vamos ver aqui:

Uma API (***Application Programming Interface***) é um conjunto de regras e protocolos que permite que diferentes sistemas ou componentes de software se comuniquem entre si. Ela define como as solicitações e respostas devem ser estruturadas, permitindo que aplicações troquem dados e funcionalidades de maneira padronizada. Por exemplo, quando você usa um aplicativo de previsão do tempo, ele pode usar uma API para buscar dados de um servidor remoto e exibi-los no seu dispositivo.

As APIs são amplamente utilizadas em desenvolvimento web e móvel para integrar serviços externos ou conectar diferentes partes de um sistema. Elas podem ser baseadas em protocolos como HTTP (para APIs RESTful) ou tecnologias como GraphQL. Uma API bem projetada simplifica o desenvolvimento, pois os desenvolvedores não precisam criar funcionalidades do zero, podendo reutilizar serviços já existentes.

Uma API funciona como uma "ponte" entre sistemas, permitindo que eles trabalhem juntos de forma eficiente. Ela é muito utilizada para a integração de serviços modernos, como redes sociais, pagamentos online, mapas e muito mais, tornando-se um pilar da tecnologia atual.

Agora, para nosso código:

```py
# ola-flask-api.py
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route("/ping")
def ping():
    return "pong"

@app.route('/echo', methods=['POST'])
def echo():
   return jsonify(request.json)

@app.route("/soma/<int:a>/<int:b>")
def soma(a, b):
    return jsonify({"resultado": a + b})

@app.route("/subtracao/<int:a>/<int:b>")
def subtracao(a, b):
    return jsonify({"resultado": a - b})

@app.route("/multiplicacao")
def multiplicacao():
    a = int(request.args.get("a"))
    b = int(request.args.get("b"))
    return jsonify({"resultado": a * b})

@app.route("/divisao", methods=["POST"])
def divisao():
    dados = request.json
    a = int(dados.get("a"))
    b = int(dados.get("b"))
    return jsonify({"resultado": a / b})

```

## x. Materiais extras de estudo

Pessoal aqui vão alguns materiais de apoio que eu utilizei para construir este material:

<iframe width="560" height="315" src="https://www.youtube.com/embed/zdgYw-3tzfI?si=4vk8JWmVuUIZRKHn" title="Web Programming with Flask - Intro to Computer Science - Harvard's CS50 (2018)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/1_nQ5A2HcgU?si=17CVHWfZL7CvwRdQ" title="API REST - Live de Python #175" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/zsYIw6RXjfM?si=8GJAgsm4HXQImMDC" title="Create A Python API in 12 Minutes" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/mt-0F_5KvQw?si=i6Eh_6RYMLCQacAj" title="Build APIs with Flask (the right way)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>