---
title: Flask
sidebar_position: 1
slug: /flask
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

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

Nesse ponto, podemos executar nossa aplicação com o comando: 

```sh
python3 -m flask --app ola-flask-api run --host 0.0.0.0 --port 8000
```

Um ponto diferente aqui é que nossa aplicação agora possui rotas que podem receber requisições e retornar respostas. Ele não é uma aplicação web tradicional, mas sim uma API, que pode ser acessada por outros sistemas através de requisições HTTP.

> ***IMPORTANTE:*** Uma aplicação pode possuir rotas de API e rotas de aplicação web. As rotas de API são utilizadas para fornecer dados e funcionalidades para outros sistemas, enquanto as rotas de aplicação web são utilizadas para fornecer uma interface interativa para o usuário.

Para testar a nossa aplicação, vamos utilizar o algum cliente para testar API, como [Postman](https://www.postman.com/), [Thunder Client](https://www.thunderclient.com/) ou o [Bruno](https://www.usebruno.com/).

Agora vamos fazer algumas requisições para a nossa aplicação. Primeiro, vamos fazer uma requisição GET para a rota `/ping`. Em seguida, vamos fazer uma requisição POST para a rota `/echo` com o corpo `{"mensagem": "Ola Mundo!!"}`. Por fim, vamos fazer requisições para as rotas `/soma`, `/subtracao`, `/multiplicacao` e `/divisao` com os parâmetros e corpo especificados.

Agora devemos configurar nossa requisição, em especial para qual rota vamos fazer ela. Além da , vale destacar que também devemos configurar outros parâmetros para nossa requisição, como o método HTTP que vamos utilizar, se algum cabeçalho ou corpo da mensagem serão enviados. Vamos testar primeiro a rota `/ping`.


Vale observar aqui alguns pontos importantes:

- O método HTTP que foi utilizado foi o `GET`, a requisição foi realizada para a rota `http://localhost:8000/ping`.
- O servidor respondeu essa requisição com o a mensagem `pong` e com **status code** 200, indicando que ela foi bem sucedida. Para mais mensagens de status do protocolo HTTP, verificar este [link😺](https://http.cat/), ou este [link🐶](https://http.dog/) ou este último por fim [link🛜](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).


Se modificarmos está requisição para tentar acessar a rota `/echo`. O método chato 🌋!! Na verdade ele está apenas indicando para nós que nossa requisição não tem os parâmetros que ele precisa para conseguir ser realizado com sucesso. Vamos ajustar nossa requisição para que ela possa trazer em seu corpo um mensagem como a rota espera. Para isso, vamos adicionar um `Body` a requisição. O corpo das requisições `POST` não é enviado como os argumentos passados como parâmetros de uma requisição `GET`, por exemplo.

:::danger[Corpo da Requisição]

Mesmo que o conteúdo da requisição seja um JSON, ele não é enviado como um parâmetro da requisição, mas sim como um corpo da requisição. Isso é importante para que o servidor consiga interpretar corretamente a requisição e retornar a resposta esperada. Devemos configurar o `Content-Type` da requisição para `application/json` e o corpo da requisição deve ser um JSON válido.

Ainda assim, isso não faz com que os dados enviados na requisição estejam protegidos por algum tipo de criptográfia, por exemplo. Para isso, devemos utilizar o protocolo HTTPS, que é uma versão segura do protocolo HTTP. Mesmo assim, diversas aplicações ainda utilizando algum algoritmo de criptografia para proteger os dados enviados e recebidos.

Para estudar mais sobre o protocolo HTTP:

<iframe width="600" height="480" max-width="80vw" src="https://www.youtube.com/embed/aumDleTg_UQ?si=S_8iCnSvNKEqwAcD" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen style={{display: 'block', marginLeft: 'auto', maxHeight: '80vh', marginRight: 'auto', marginBottom: '16px'}}></iframe>

<iframe width="600" height="480" max-width="80vw" src="https://www.youtube.com/embed/iYM2zFP3Zn0?si=-2uDhm_PhEKsB0Wk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen style={{display: 'block', marginLeft: 'auto', maxHeight: '80vh', marginRight: 'auto', marginBottom: '16px'}}></iframe>

:::

Continuando com os testes das nossas rotas, os métodos `soma` e `subtracao` são rotas que recebem parâmetros na URL. Já os métodos `multiplicacao` e `divisao` recebem parâmetros no corpo da requisição. Vamos testar cada uma delas. Primeiro os métodos `soma` e `subtracao`.

Podemos observar que os parâmetros para essas rotas são passados diretamente na URL. Já para a rota `multiplicacao`, os parâmetros devem ser passados como `Query String`, ou seja, como parâmetros passados na URL, mas que não fazem parte da rota. Vamos passar a `Query String` para a rota `multiplicacao`, enviando eles depois da rota, separados por `?` e `&`.

Por fim, a rota `divisao` recebe os parâmetros no corpo da requisição, como um JSON. Vamos configurar a requisição para que ela possa ser realizada com sucesso.

Pessoal, desta forma abordamos diferentes aspectos de uma aplicação web, como ela pode ser construída e como podemos testar ela. Vamos continuar com a construção da nossa aplicação, mas antes, vamos fazer uma pausa para o café ☕☕. Na sequencia, vamos continuar com a construção da nossa aplicação web.

## 5. Construção de uma aplicação web com Flask

Agora, vamos construir nossa aplicação Web utilizando um outro recurso do Flask, os *templates*. Os *templates* são arquivos HTML que contém o código HTML da interface da aplicação. Elas são utilizadas para criar páginas da aplicação que o usuário visualiza, como a página inicial, a página de produtos e a página de checkout. Os *templates* permitem que possamos criar páginas dinâmicas, que podem exibir diferentes conteúdos com base nos dados da aplicação.

Na nossa solução, vamos criar o diretório `templates` e o arquivo `app.py`, na raiz do diretório da solução. Em seguida, vamos adicionar o seguinte código ao arquivo `app.py`:

```python
# app.py
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```

Dentro do diretório `templates`, vamos criar o arquivo `index.html` e adicionar o seguinte código:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Minha Aplicação Web</title>
</head>
<body>
    <h1>Ola Mundo!!</h1>
</body>
</html>
```

Como modificamos nosso arquivo `app.py`, vamos executar nossa aplicação com o comando: 

```sh
`python3 app.py
```
Agora, ao acessar a rota `http://localhost:8000`, vamos ver a página `index.html` sendo exibida no navegador.

Mais arquivos e outras rotas podem ser adicionados a aplicação. Vamos adicionar mais uma rota e um arquivo HTML para ela. Vamos criar o arquivo `sobre.html` e adicionar o seguinte código:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Sobre</title>
</head>
<body>
    <h1>Sobre</h1>
    <p>Esta é a página sobre a minha aplicação web.</p>
</body>
</html>
```

E adicionar a rota para a página `sobre.html` no arquivo `app.py`:

```python
# app.py
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/sobre")
def sobre():
    return render_template("sobre.html")

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```

Agora, ao acessar a rota `http://localhost:8000/sobre`, vamos ver a página `sobre.html` sendo exibida no navegador.

> "Mas Murilão, e se eu quisar passar informações para a página, como eu faço?". Podemos preparar nossa aplicação para receber informações e passar elas para a página. Vamos adicionar um parâmetro para a rota `sobre` e passar ele para a página `sobre.html`. Vamos adicionar o seguinte código ao arquivo `app.py`:

```python
# app.py
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/sobre/<nome>")
def sobre(nome):
    return render_template("sobre.html", nome=nome)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)	
```

Aqui estamos passando um parâmetro para a rota `sobre` e passando ele para a página `sobre.html`. Agora, ao acessar a rota `http://localhost:8000/sobre/Murilão`, vamos ver a página `sobre.html` sendo exibida no navegador com as mensagens: 

> Esta é a página sobre a minha aplicação web.
> Ola Murilão!!

Para isso, é necessário editar o arquivo `sobre.html`. Vamos adicionar o seguinte código:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Sobre</title>
</head>
<body>
    <h1>Sobre</h1>
    <p>Esta é a página sobre a minha aplicação web.</p>
    <p>Ola {{ nome }}!!</p>
</body>
</html>
```

> "Calma lá Murilão! Que aconteceu aqui? Tem umas coisas nesse código que não são HTML!" Isso mesmo pessoal, o código que está entre `{{` e `}}` é um código Python que é executado pelo Flask. Esse código é utilizado para passar informações da aplicação para a página. O código `{{ nome }}` é utilizado para exibir o valor da variável `nome` na página. O Flask substitui o código `{{ nome }}` pelo valor da variável `nome` antes de enviar a página para o navegador. Esse tipo de código é chamado de *template tag* e é utilizado para criar páginas dinâmicas com o Flask. Quem quiser saber mais sobre *template tags*, acesse [aqui](https://flask.palletsprojects.com/en/latest/templating/). A biblioteca utilizada para isso é a Jinja2, que é uma biblioteca de *template* para Python. Para conhecer mais sobre a Jinja2, acesse [aqui](https://jinja.palletsprojects.com/en/latest/).

Legal, agora conseguimos ajustar nossa aplicação para que ela possa enviar informações de uma página para outra. Vamos utilizar um `form` para enviar informações da página para a aplicação. Na rota `\`, vamos adicionar um formulário que envia informações para a rota `/sobre`. Vamos adicionar o seguinte código ao arquivo `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Minha Aplicação Web</title>
</head>
<body>
    <h1>Ola Mundo!!</h1>
    <form action="/sobre" method="post">
        <input type="text" name="nome" placeholder="Digite o seu nome">
        <button type="submit">Enviar</button>
    </form>
</body>
</html>
```
Se apenas fizermos está modificação, não vamos conseguir enviar as informações para a rota `/sobre`. Isso porque a rota `/sobre` está configurada para receber apenas requisições do tipo `GET`. Vamos ajustar a rota `/sobre` para que ela possa receber requisições do tipo `POST` também. Não vamos deixar de receber requisições do tipo `GET`, mas vamos adicionar a possibilidade de receber requisições do tipo `POST`. Vamos adicionar o seguinte código ao arquivo `app.py`:

```python
# app.py
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/sobre", methods=["GET", "POST"])
def sobre(nome=None):
    if request.method == "POST":
        nome = request.form.get("nome")
    return render_template("sobre.html", nome=nome)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```

Aqui tem algumas coisas que valem a pena observar:
- A função `sobre` agora recebe um parâmetro `nome` com o valor padrão `None`. Isso é feito para que a função possa ser chamada com ou sem o parâmetro `nome`.
- A função `sobre` verifica o método da requisição utilizando `request.method`. Se o método da requisição for `POST`, a função obtém o valor do campo `nome` do formulário utilizando `request.form.get("nome")`. Se o método da requisição for `GET`, a função utiliza o valor padrão `None` para o parâmetro `nome`.
- Quando a função `sobre` recebe uma requisição do tipo `GET` apenas, ela retorna a página `sobre.html` com o valor padrão `None` para o parâmetro `nome`.

Agora que já estamos conseguindo enviar informações entre as páginas, vamos adicionar algumas imagens e estilos para a nossa aplicação. Vamos criar o diretório `static` dentro do diretório `projeto-web` e adicionar o arquivo `style.css` e as imagens `logo.png` e `background.png`. Em seguida, vamos adicionar o seguinte código ao arquivo `style.css`:

```css
/* style.css */
body {
    background-image: url("/static/background.png");
    background-size: cover;
    color: white;
    font-family: Arial, sans-serif;
}

h1 {
    text-align: center;
    margin-top: 100px;
    font-size: 3em;
    color: #313131;
}

form {
    text-align: center;
    margin-top: 50px;
}

input {
    padding: 10px;
    font-size: 1.5em;
}

button {
    padding: 10px;
    font-size: 1.5em;
}
```

E adicionar o seguinte código ao arquivo `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Minha Aplicação Web</title>
    <link rel="icon" href="{{ url_for('static', filename='logo.png') }}" sizes="16x16 32x32 48x48">
    <link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>Ola Mundo!!</h1>
    <form action="/sobre" method="post">
        <input type="text" name="nome" placeholder="Digite o seu nome">
        <button type="submit">Enviar</button>
    </form>
</body>
</html>
```

Repare que mudamos a aplicação para que ela possa carregar o arquivo `style.css` e as imagens `logo.png` e `background.png`. Para isso, utilizamos a função `url_for` para gerar os URLs dos arquivos estáticos. A função `url_for` é utilizada para gerar URLs para as rotas da aplicação e para os arquivos estáticos. Para conhecer mais sobre a função `url_for`, acesse [aqui](https://flask.palletsprojects.com/en/latest/api/#flask.url_for).

Agora vamos editar que o nosso projeto para que ele possa receber textos de uma página e salve esses dados no banco de dados.

## 6. Deploy da aplicação web

Primeiro vamos compreender o que é o processo de deploy. O deploy é o processo de implantar a aplicação em um servidor de produção. O servidor de produção é um servidor que está configurado para executar a aplicação de forma segura e eficiente. O servidor de produção é utilizado para atender as requisições dos usuários finais e fornecer uma experiência interativa ao usuário. O deploy é um processo crítico que requer planejamento e execução cuidadosa. O deploy é uma parte importante do ciclo de vida da aplicação e deve ser realizado com cuidado e atenção.

> "Nossa Murilão, que monte de palavras bonitas, mas o que elas significam?" Quando temos nossa aplicação, ela está funcionando no nosso computador apenas. Quando vamos colocar a aplicação em produção, nosso objetivo é deixar ela disponível para que outras pessoas possam utilizar nosso sistema.

Primeiro precisamos instalar um servidor WSGI, como o Gunicorn ou o uWSGI. O servidor WSGI é um servidor que executa a aplicação de forma segura e eficiente. Ele é utilizado para atender as requisições dos usuários finais e fornecer uma experiência interativa ao usuário. para saber mais sobre o Gunicorn, acesse [aqui](https://gunicorn.org/). Em seguida, vamos instalar o Gunicorn com o comando `pip install gunicorn`. 

Vamos executar nossa aplicação com o comando `gunicorn projeto-web.app:app`. O comando `gunicorn projeto-web.app:app` é utilizado para executar a aplicação com o Gunicorn. O argumento `projeto-web.app:app` é utilizado para especificar o nome do arquivo que contém a aplicação e o nome da instância da classe `Flask`.

:::danger[Não Compatível com Windows]

O Gunicorn não é compatível com o Windows. Como o processo de deploy, em geral, ocorre em sistemas operacionais Linux, não é um problema para a maioria dos casos. No entanto, se você estiver utilizando o Windows, pode ser necessário utilizar uma máquina virtual ou um contêiner para executar o Gunicorn.

:::

Agora vamos realizar o freeze da nossa aplicação para que possamos criar um arquivo `requirements.txt` com as dependências da nossa aplicação. Para isso, vamos utilizar o comando `pip freeze > requirements.txt`. O comando `pip freeze` é utilizado para listar todas as dependências da aplicação. O operador `>` é utilizado para redirecionar a saída do comando `pip freeze` para o arquivo `requirements.txt`.

Agora vamos criar um arquivo chamado `Procfile` e adicionar o seguinte código:

```txt
web: gunicorn projeto-web.app:app
```

O arquivo `Procfile` é utilizado para especificar os comandos que devem ser executados para iniciar a aplicação. O comando `web: gunicorn projeto-web.app:app` é utilizado para iniciar a aplicação com o Gunicorn.

Agora vamos acessar o site [render.com](https://render.com/). Ele vai permitir realizar o deploy da nossa aplicação utilizando o plano gratuito. Vamos criar uma conta no site e seguir as instruções para realizar o deploy da nossa aplicação. Na [página](https://dashboard.render.com/register?next=%2F), escolher uma das formas para realizar o login na plataforma. Uma vez logado na plataforma, vamos escolher a opção `New` e em seguida `Web Service`.

<img src={useBaseUrl("img/deploy-render/inicio-render.png")} alt="Requisição para a rota /echo" style={{ display: 'block', marginLeft: 'auto', maxHeight: '80vh', marginRight: 'auto', marginBottom: '16px' }} />

Agora vamos selecionar que desejamos realizar o deploy de um repositório do Github. Aqui cabe destacar que pode ser utilizada outra plataforma de versionamento, mas por hora vamos focar no Github.

<img src={useBaseUrl("img/deploy-render/escolhendo-fonte.png")} alt="Requisição para a rota /echo" style={{ display: 'block', marginLeft: 'auto', maxHeight: '80vh', marginRight: 'auto', marginBottom: '16px' }} />

Agora devemos realizar a escolha do repositório que vamos fazer o deploy. Para este exemplo, vou utilizar o repositório da disciplina.

<img src={useBaseUrl("img/deploy-render/escolha-repositorio.png")} alt="Requisição para a rota /echo" style={{ display: 'block', marginLeft: 'auto', maxHeight: '80vh', marginRight: 'auto', marginBottom: '16px' }} />

Depois do repositório selecionado, devemos escolher e configurar a *branch* que vamos utilizar para o deploy. Aqui, vamos utilizar a *branch* `main` e vamos configurar a plataforma para realizar o deploy sempre que houver uma alteração na *branch*. Outro ponto importante para se configurar é de onde a aplicação está sendo construída para o deploy. Como nosso repositório não possui apenas a aplicação que queremos fazer o deploy, vamos configurar a plataforma para que ela saiba onde está a aplicação que queremos fazer o deploy.

<img src={useBaseUrl("img/deploy-render/configurando-deploy.png")} alt="Requisição para a rota /echo" style={{ display: 'block', marginLeft: 'auto', maxHeight: '80vh', marginRight: 'auto', marginBottom: '16px' }} />

Agora vamos configurar para utilizar a instância gratuita da plataforma. Para isso, vamos escolher a opção `Free` e em seguida `Create Web Service`.

<img src={useBaseUrl("img/deploy-render/selecionando-instancia.png")} alt="Requisição para a rota /echo" style={{ display: 'block', marginLeft: 'auto', maxHeight: '80vh', marginRight: 'auto', marginBottom: '16px' }} />

:::danger[Sem Disco de Persistência]

Na versão gratuíta da plataforma, não é possível utilizar um disco de persistência. Isso significa que os dados que são salvos na aplicação não são mantidos entre as execuções da aplicação. Isso é importante e relevante para nossa validação. No formato que estamos trabalhando, atualmente, isso significa que depois de um tempo de execução, nossa aplicação ficará sem seus registros.

:::

Pessoal, desta forma conseguimos realizar o deploy da nossa aplicação. Ela ainda pode ser melhorada com implementação de responsividade, melhoria na interface e na experiência do usuário. 


## 7. Melhorando nossa aplicação

Pessoal agora vamos considerar algumas coisas:

- Por enquanto, toda nossa aplicação está em um arquivo só, já podemos desconfiar que essa arquitetura não parece escalar;
- Ainda quanto o problema de estar com um arquivo fonte apenas, se mais de um desenvolvedor for trabalhar no arquivo, vamos precisar lidar com conflitos constantes na hora de unificar este arquivo;
- Todo nosso código começa a ficar dificíl de ser reaproveitado.

> Mas Murilão tem alguma ferramenta que podemos utilizar para resolver isso?

Opa! Temos uma solução para isso sim! Podemos utilizar os `Blueprints` do próprio Flask! Vamos verificar como utilizar esse recurso. Para isso, vamos trabalhar com a seguinte aplicação:


```python
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/calcular', methods=['POST'])
def calculate():
    data = request.get_json()
    
    if not data or 'num1' not in data or 'num2' not in data or 'operation' not in data:
        return jsonify({'error': 'Campos inválidos'}), 400
    
    num1 = data.get('num1')
    num2 = data.get('num2')
    operation = data.get('operation')

    if not isinstance(num1, (int, float)) or not isinstance(num2, (int, float)):
        return jsonify({'error': 'Os valores devem ser números'}), 400
    
    result = None

    if operation == 'add':
        result = num1 + num2
    elif operation == 'subtract':
        result = num1 - num2
    elif operation == 'multiply':
        result = num1 * num2
    elif operation == 'divide':
        if num2 == 0:
            return jsonify({'error': 'Divisão por zero não permitida'}), 400
        result = num1 / num2
    else:
        return jsonify({'error': 'Operação inválida'}), 400

    return jsonify({'num1': num1, 'num2': num2, 'operation': operation, 'result': result})


@app.route('/convert', methods=['POST'])
def convert():
    data = request.get_json()

    if not data or 'value' not in data or 'unit' not in data:
        return jsonify({'error': 'Campos inválidos'}), 400
    
    value = data.get('value')
    unit = data.get('unit').lower()

    if not isinstance(value, (int, float)):
        return jsonify({'error': 'O valor deve ser um número'}), 400

    if unit == 'inches':
        result = value * 25.4
        new_unit = 'mm'
    elif unit == 'mm':
        result = value / 25.4
        new_unit = 'inches'
    else:
        return jsonify({'error': 'Unidade inválida. Use "inches" ou "mm".'}), 400

    return jsonify({'original_value': value, 'original_unit': unit, 'converted_value': result, 'converted_unit': new_unit})


if __name__ == '__main__':
    app.run(debug=True)

```

Aqui pessoal, temos algumas coisas para ver neste código:

- Temos duas rotas na nossa aplicação: `/calcular` e `/convert`, ambas funcionam com requisições do tipo POST. Ambas funcionam recebendo os dados dentro do body enviados como JSON.
- Aqui, ambos os métodos fazem algumas verificações para garantir que todos os parâmetros necessários para funcionar. Se estes parâmetros não estão presentes, o método retorna um erro para quem o invocou.
- Nossa API recebe e envia dados no formato JSON.

Agora vamos para os `Blueprints`.

## 8. Blueprints - uma forma de dividir nossa aplicação

Primeiro, vamos verficar a documentação dos Blueprints: [doc](https://flask.palletsprojects.com/en/stable/blueprints/). Um ponto muito importante para verificarmos:

> "***The basic concept of blueprints is that they record operations to execute when registered on an application. Flask associates view functions with blueprints when dispatching requests and generating URLs from one endpoint to another.***"

Este é o conceito da utilização dos blueprints: dividir a aplicação em partes menores e associar elas com a aplicação principal.

Vamos agora utilizar este princípio para realizar a separação da nossa aplicação. Primeiro vamos criar mais dois diretórios da aplicação:

```sh
# Estrutura de Arquivos
├── calculadora
│   ├── calculadora.py
│   └── __init__.py
├── conversor
│   ├── conversor.py
│   └── __init__.py
├── main.py
└── venv

```

:::info[Arquivo __init__.py]

Em Python, um diretório só é reconhecido como um pacote se ele contiver um arquivo __init__.py. Esse arquivo indica ao interpretador Python que o diretório deve ser tratado como um módulo, permitindo que seus arquivos sejam importados como parte do pacote.

> Por que o __init__.py é necessário?

- Identifica um diretório como um pacote – Sem ele, o Python não reconhecerá o diretório como um módulo importável.
- Executa inicializações do pacote – Pode conter código de inicialização, como importações internas ou configuração de variáveis globais.
- Organiza código modularmente – Facilita a estruturação de projetos grandes, dividindo funcionalidades em subpacotes.


Dada a seguinte estrutura:

```sh
my_project/
│── my_package/
│   │── __init__.py
│   │── module1.py
│   │── module2.py
```

Com __init__.py presente, podemos fazer:

```py
from my_package import module1
```

Caso ele não existisse, o Python não reconheceria my_package como um pacote importável (exceto em versões mais recentes, onde os namespace packages foram introduzidos).

> ***Curiosidade:***
> Desde o Python 3.3, o __init__.py não é obrigatório para pacotes, mas sua presença ainda é recomendada para evitar ambiguidades e permitir personalizações. 🚀

:::

Vamos agora ajustar o arquivo ***calculadora.py***

```python
from flask import Blueprint, request, jsonify

calculadora = Blueprint('calculadora', __name__,
                        template_folder='templates',
                        url_prefix='/calcular')


@calculadora.route('/', methods=['POST'])
def calculate():
    data = request.get_json()
    
    if not data or 'num1' not in data or 'num2' not in data or 'operation' not in data:
        return jsonify({'error': 'Campos inválidos'}), 400
    
    num1 = data.get('num1')
    num2 = data.get('num2')
    operation = data.get('operation')

    if not isinstance(num1, (int, float)) or not isinstance(num2, (int, float)):
        return jsonify({'error': 'Os valores devem ser números'}), 400
    
    result = None

    if operation == 'add':
        result = num1 + num2
    elif operation == 'subtract':
        result = num1 - num2
    elif operation == 'multiply':
        result = num1 * num2
    elif operation == 'divide':
        if num2 == 0:
            return jsonify({'error': 'Divisão por zero não permitida'}), 400
        result = num1 / num2
    else:
        return jsonify({'error': 'Operação inválida'}), 400

    return jsonify({'num1': num1, 'num2': num2, 'operation': operation, 'result': result})

```

Pontos importantes para verificar neste código:
- Blueprint('calculadora', __name__): Cria um Blueprint chamado "calculadora".
- template_folder='templates': (Opcional) Define um diretório para templates (não usado neste código).
- url_prefix='/calcular': Todas as rotas definidas dentro desse Blueprint terão /calcular como prefixo. Exemplo:O endpoint / definido no código será acessado como /calcular/.

Agora vamos alterar o código ***conversor.py***:

```py
from flask import Blueprint, request, jsonify

conversor = Blueprint('conversor', __name__,
                        template_folder='templates',
                        url_prefix='/convert')


@conversor.route('/', methods=['POST'])
def convert():
    data = request.get_json()

    if not data or 'value' not in data or 'unit' not in data:
        return jsonify({'error': 'Campos inválidos'}), 400
    
    value = data.get('value')
    unit = data.get('unit').lower()

    if not isinstance(value, (int, float)):
        return jsonify({'error': 'O valor deve ser um número'}), 400

    if unit == 'inches':
        result = value * 25.4
        new_unit = 'mm'
    elif unit == 'mm':
        result = value / 25.4
        new_unit = 'inches'
    else:
        return jsonify({'error': 'Unidade inválida. Use "inches" ou "mm".'}), 400

    return jsonify({'original_value': value, 'original_unit': unit, 'converted_value': result, 'converted_unit': new_unit})

```

Repare que fizemos a mesma alteração que no ***calculadora.py***. Mas todo o conteúdo está relacionado ao módulo do conversor! Assim estamos com os dois módulos separados!!

Vamos agora verificar como fica nosso ***main.py***:

```py
from flask import Flask
from calculadora.calculadora import calculadora
from conversor.conversor import conversor

app = Flask(__name__)
app.register_blueprint(calculadora)
app.register_blueprint(conversor)

if __name__ == '__main__':
    app.run(debug=True)

```

O que fizemos aqui é iniciar nossa aplicação e ligar os blueprints a ela! Denovo! Deixamos nossa aplicação:
- Modular: estamos adicionando os blueprints que desejamos utilizar;
- Reutilizavel: os módulos que construímos podemos reaproveitar e utilizar outros módulos no projeto, bastando adicionar este blueprint.

Pessoal sugiro que vocês verifiquem e modifiquem este exemplo! Explorem como está abordagem pode ser utilizada para dar outra forma a nossas aplicações. Bons estudos pessoal!!


## 9. Materiais extras de estudo

Pessoal aqui vão alguns materiais de apoio que eu utilizei para construir este material:

<iframe width="560" height="315" src="https://www.youtube.com/embed/zdgYw-3tzfI?si=4vk8JWmVuUIZRKHn" title="Web Programming with Flask - Intro to Computer Science - Harvard's CS50 (2018)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/1_nQ5A2HcgU?si=17CVHWfZL7CvwRdQ" title="API REST - Live de Python #175" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/zsYIw6RXjfM?si=8GJAgsm4HXQImMDC" title="Create A Python API in 12 Minutes" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/mt-0F_5KvQw?si=i6Eh_6RYMLCQacAj" title="Build APIs with Flask (the right way)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>