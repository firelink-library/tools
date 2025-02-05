---
title: CLI Python
sidebar_position: 2
slug: /cli-python
---

## 1. Command Line Interface - Refresh

Pessoal, apenas como uma retomada: aplicações de linha de comando são aquelas executadas com uma interface de texto. O usuário pode interagir de algumas formas distintas: enviando parâmetros ou interagindo com a aplicação.

:::tip[Para saber mais]

<details> 
    <summary mdxType="summary">	CLI (A "temida" Command Line Interface) // Dicionário do Programador</summary>

    - https://youtu.be/8AgOxHOAV9Y?si=KCqZ1wCncLg--OjU&t=130
</details> 
<details> 
    <summary mdxType="summary">	O que é uma aplicação COMMAND-LINE (CLI)?</summary>

    - https://www.youtube.com/watch?v=-CJr6afTy-0
</details> 
<details> 
    <summary mdxType="summary">	Professional CLI Applications with Click</summary>

    - https://www.youtube.com/watch?v=vm9tOamPkeQ
</details> 
<details> 
    <summary mdxType="summary">	5 Python Libraries for Building Command Line Tools</summary>

    - https://www.youtube.com/watch?v=20Qkq93kwKw
</details> 
<details> 
    <summary mdxType="summary">	Criando aplicações de linha de comando (CLIs) com Typer | Live de Python #233</summary>

    - https://www.youtube.com/watch?v=m1_48lmAX-Y
</details> 

:::

Vamos agora iniciar a preparação para realizar nosso trabalho.

## 2. Criando o Ambiente Virtual

A estrutura de diretórios que vamos utilizar é a seguinte:

```bash
.
├── .gitignore
├── README.md
├── src
```
Todos estes arquivos podem ser encontrados no diretório [encontro-3-computacao](#). O que cada um destes diretórios e arquivos significam? Vamos avaliar eles em conjunto:

- `.gitignore`: Este arquivo é utilizado para que o git ignore arquivos que não são necessários para o versionamento do projeto. Por exemplo, arquivos de configuração, arquivos de log, arquivos temporários, etc. É importante colocar estes arquivos no `.gitignore` para que o git não fique "poluído" com arquivos que não são necessários.
- `README.md`: Este arquivo é utilizado para que possamos documentar o projeto. É importante que este arquivo seja bem escrito e que contenha todas as informações necessárias para que qualquer pessoa que entre no projeto consiga entender o que está acontecendo. Em especial quando estamos utilizando ambientes virtuais ou alguma outra dependência que não está no projeto, ele deve descrever o que uma pessoal deve fazer para conseguir utilizar nosso projeto.
- `src`: Este diretório é onde vamos colocar o código fonte do nosso projeto. É importante que ele seja bem organizado e que siga as boas práticas de programação.

:::danger[Atenção]

Pessoal deste ponto em diante estou considerando que os comandos para executar nosso ambiente virtual serão executados no terminal do seu sistema operacional. Se você estiver utilizando o Windows, abra o `cmd` (na teoria o `PowerShell` deve funcionar também). Se você estiver utilizando o Linux ou o MacOS, abra o terminal do seu sistema operacional.

Em alguns sistemas operacionais, o comando `python` invoca a versão do Python 2. Se você estiver utilizando o Python 3, você deve utilizar o comando `python3`. Se você não souber qual é a versão do Python que você está utilizando, basta executar o comando `python --version` ou `python3 --version` no terminal. Se você estiver utilizando o Python 3, substitua o comando `python` por `python3` nos comandos a seguir.

Se o terminal do Windows não estiver reconhecendo o comando `python`, você pode tentar adicionar o Python nas variáveis de ambiente do Windows. Se você não souber como fazer isso, você pode seguir [este tutorial](https://docs.python.org/pt-br/3/using/windows.html#excursus-setting-environment-variables).

:::

Agora que temos a estrutura do nosso projeto, vamos criar um ambiente virtual para ele. Para isso, vamos utilizar a ferramenta `venv` que já vem com o Python. Para criar um ambiente virtual, basta executar o seguinte comando:

```bash
python3 -m venv venv
```

Este comando vai criar um ambiente virtual na pasta `venv`. E o que isso significa? Que estamos criando um ambiente dedicado para trabalhar com Python para o nosso projeto. Outras dependências que não estão no Python, não vão ser instaladas no Python global, mas sim no Python do ambiente virtual. Isso é importante para que possamos ter um ambiente isolado e que não interfira em outros projetos.

Após a criação do ambiente virtual, a seguinte estrutura de pasta vai surgir:

```bash
.
├── .gitignore
├── README.md
├── src
├── venv
```

Dentro do diretório `venv` temos a seguinte estrutura:

```bash
.
├── bin
├── include
├── lib
├── pyvenv.cfg
└── share
```

:::tip[Dica]

A estrutura de diretórios do ambiente virtual pode variar de acordo com o sistema operacional que você está utilizando. Por exemplo, no Windows, o diretório `bin` é substituído por `Scripts`. No MacOS, o diretório `lib` é substituído por `libexec`. No Linux, o diretório `lib` é substituído por `lib64`.

:::

Para ativar este ambiente virtual, basta executar o seguinte comando:

```bash
source venv/bin/activate
```

:::tip[Dica]

A forma de ativar o ambiente virtual pode variar de acordo com o sistema operacional que você está utilizando. No Windows, o comando para ativar o ambiente virtual é `venv\Scripts\activate`. No MacOS, o comando para ativar o ambiente virtual é `source venv/bin/activate`. No Linux, o comando para ativar o ambiente virtual é `source venv/bin/activate`.

:::

Após a ativação do ambiente virtual, o terminal vai mostrar o nome do ambiente virtual que está ativo. Por exemplo:

```bash
(venv) $
```

Par verificarmos a instalação do ambiente virtual, podemos executar o seguinte comando:

```bash
which python
```

A saída esperada deste comando é a pasta do ambiente virtual. Por exemplo:

```bash
/home/usuario/projeto/venv/bin/python
```

:::tip[Dica]

A saída deste comando pode variar de acordo com o sistema operacional que você está utilizando. No Windows, a saída deste comando é `C:\caminho\para\o\projeto\venv\Scripts\python.exe`. No MacOS, a saída deste comando é `/caminho/para/o/projeto/venv/bin/python`. No Linux, a saída deste comando é `/caminho/para/o/projeto/venv/bin/python`.

:::

Agora com o nosso ambiente virtual criado, vamos iniciar o processo de criar nossa aplicação 💻🖥️!!
Para isso, vamos iniciar ela com um programa básico que vamos refatorando para adicionar as funcionalidades que desejamos.

## 3. Iniciando um Programa Básico

Dentro do diretório `src`, vamos criar um arquivo chamado `main.py`. Este arquivo vai ser o ponto de entrada da nossa aplicação. Dentro deste arquivo, vamos adicionar o seguinte código:

```python main.py
# Este é o arquivo ponto de entrada da nossa aplicação
print('Olá, Mundo!')
print(f'Quando este arquivo é executado: {__name__}')
```

Para executar este arquivo, basta executar o seguinte comando:

```bash
python3 src/main.py
```

A saída para a execução deste arquivo é a seguinte:

```bash
Olá, Mundo!
Quando este arquivo é executado: __main__
```

:::warning[Atenção]

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcShKVTG4R617R4putDaUqG2Yg7806L8pKVsfQ&s" alt="ESPERE UM POUCO" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: 24 }} />

Muito cuidado deste ponto em diante! Em especial, porque neste momento, se você está acompanhando as aulas, deve ter passado em cabeça a seguinte afirmação:

> "Como eu escrevi código e quero manter a rastreabilidade das minhas ações, vou commitar o que eu fiz até agora."

E você ***ESTÁ ABSOLUTAMENTE CERTO***! Mas antes de fazer isso, vamos adicionar no nosso `.gitignore` o diretório `venv` para que ele não seja versionado. Isso é importante para que outras pessoas que baixarem o projeto não tenham que baixar o ambiente virtual também. Para isso, basta adicionar a seguinte linha no arquivo `.gitignore`:

```bash
venv
```

> ***MAS MURILÃO, POR QUE EU NÃO DEVO COMMITAR O AMBIENTE VIRTUAL?***
> Porque o ambiente virtual é uma dependência do projeto. E como dependência, ele não deve ser versionado. Isso porque cada pessoa que baixar o projeto pode ter uma versão diferente do Python, ou mesmo do sistema operacional. E se o ambiente virtual for versionado, pode ser que o projeto não funcione em outras máquinas.

> ***MAS MURILÃO, COMO EU FAÇO PARA QUE OUTRAS PESSOAS POSSAM EXECUTAR O MEU PROJETO?***
> Você deve adicionar um arquivo chamado `requirements.txt` na raiz do projeto. Este arquivo deve conter todas as dependências do projeto. E para que as pessoas consigam instalar estas dependências, basta que elas executem o seguinte comando:

```bash
pip install -r requirements.txt
```

> ***MAS MURILÃO, COMO EU FAÇO PARA CRIAR O ARQUIVO `requirements.txt`?***
> Você pode criar este arquivo manualmente, ou você pode utilizar o seguinte comando:

```bash
pip freeze > requirements.txt
```

Este comando vai criar um arquivo chamado `requirements.txt` com todas as dependências do projeto. 

> ***MAS MURILÃO, EU OLHEI NO SEU GITHUB E VI QUE EM UM COMMIT O SEU VENV FOI ADICIONADO. POR QUE?***
> Como vocês acham que eu lembrei de colocar esse aviso aqui?

:::

Pessoal vamos voltar para o nosso código. Se observarmos ele, o `__name__` apareceu com o valor de `__main__`. Isso acontece porque o Python atribui o valor de `__main__` para o arquivo que está sendo executado. Isso é importante para que possamos saber se o arquivo está sendo executado como um módulo ou como um arquivo principal.

Vamos fazer um teste: criar um outro arquivo e importar o nosso arquivo `main` dentro dele. Vamos chamar este arquivo de `teste_import.py`.

```python
# teste_import.py
import main
print(f'Este é o __name__ do teste_import.py: {__name__}')
```

Agora vamos executar o arquivo `teste_import.py`:

```bash
python3 src/teste_import.py
```

Vamos obter como saída:

```bash
Olá, Mundo!
Quando este arquivo é executado: main
Este é o __name__ do teste_import.py: __main__
```

Podemos reparar que o `__name__` do arquivo `main.py` é `main`, e o `__name__` do arquivo `teste_import.py` é `__main__`. Isso acontece porque o Python atribui o valor de `__main__` para o arquivo que está sendo executado. Para os demais módulo, o valor de `__name__` é o nome do módulo.

:::tip[Dica]

Vale destacar um comportamento aqui: ao importar um módulo, todo o código que está no corpo daquele módulo é executado. Isso é importante para que possamos inicializar variáveis, funções, classes, etc. que são necessárias para o funcionamento do módulo.

:::

Agora vamos iniciar a criação da nossa CLI. Quando estamos executando uma CLI, podemos ter diferentes comportamentos de acordo com os argumentos que são passados para ela. Por exemplo, se executarmos o comando `ls` no terminal, ele vai listar os arquivos e diretórios do diretório atual. Se executarmos o comando `ls -l`, ele vai listar os arquivos e diretórios do diretório atual, mas com mais informações. Se executarmos o comando `ls -a`, ele vai listar os arquivos e diretórios do diretório atual, mas com os arquivos ocultos. E assim por diante.

Vamos focar nesse tipo de solução por hora, onde enviamos os parâmetros para a execução do nosso programa. Vamos iniciar criando um programa que realiza a soma de dois números. Vou alterar nosso programa `main.py`.

```python
# main.py
import sys

# Vamos configurar está função main() para ser executada apenas quando o script for o ponto de entrada da aplicação
def main():
    # Nome do script
    print(f'Nome do Script: {sys.argv[0]}')

    # Somando os demais elementos do script
    soma = 0
    for elemento in sys.argv[1:]:
        soma += float(elemento)
    print(f'Soma dos elementos fornecidos: {soma}')

if __name__ == "__main__":
    main()
```

Vamos executar primeiro o nosso script com o comando: `python3 src/main.py`, para obter a seguinte saída na tela:

```bash
Nome do Script: src/main.py
Soma dos elementos fornecidos: 0
```

Vamos executar o script novamente, mas agora fornecendo alguns valores para ele:

```bash
python3 src/main.py 1 2.3 4 5 6
```

A saída que vamos obter agora é:

```bash
Nome do Script: src/main.py
Soma dos elementos fornecidos: 18.3
```

## 4. Aplicação CLI

Agora será que podemos melhorar essa nossa interação com a CLI? ***Sim*** ou ***Com Certeza***? Vamos atualizar nosso sistema para utilizar a biblioteca [`Typer`](https://typer.tiangolo.com/). 

> ***MAS MURILÃO, POR QUE EU DEVO UTILIZAR O TYPER?***
> O `Typer` é uma biblioteca que nos ajuda a criar CLIs de forma rápida e fácil. Ele é baseado no `click`, mas com a diferença de que ele é mais rápido e mais fácil de utilizar. Além disso, ele é baseado no `Python 3.6+` e utiliza as `type hints` para criar a interface da CLI. Ela foi desenvolvida pelo [Sebastián Ramírez](https://tiangolo.com/), o mesmo desenvolvedor do `FastAPI`.

Para instalar o `Typer`, basta executar o seguinte comando:

```bash
pip install "typer[all]"
```

Isso vai instalar o `Typer` no ambiente virtual do projeto. Agora vamos atualizar o nosso arquivo `main.py` para utilizar o `Typer`.

```python
# main.py
import typer

# Vamos configurar está função main() para ser executada apenas quando o script for o ponto de entrada da aplicação
def main(valor1: float, valor2: float):
    # Somando os demais elementos do script
    soma = valor1 + valor2
    print(f'Soma dos elementos fornecidos: {soma}')

if __name__ == "__main__":
    typer.run(main)
```

Agora vamos executar o nosso script com o comando: `python3 src/main.py`, para obter a seguinte saída na tela:

```bash
Usage: main.py [OPTIONS] VALOR1 VALOR2
Try 'main.py --help' for help.
Error: Missing argument 'VALOR1'.
```

O que o terminal está mostrando para nós agora é que estamos utilizando a biblioteca `Typer` para criar a nossa CLI. E que estamos utilizando dois argumentos para a execução do nosso script. Vamos executar o script novamente, mas agora fornecendo os valores para ele:

```bash
python3 src/main.py 1 2.3
```

A saída que vamos obter agora é:

```bash
Soma dos elementos fornecidos: 3.3
```

Vamos atualizar as dependencias do nosso projeto. Para isso, vamos criar uma nova versão do arquivo chamado `requirements.txt` na raiz do projeto. Este arquivo deve conter todas as dependências do projeto. 

```bash
python3 -m pip freeze > requirements.txt
```

Agora vamos deixar nosso projeto mais sofisticado. Vamos criar um comando para a nossa CLI. Vamos criar um comando que realiza a soma e outro que realiza a subtração de dois números. Vamos alterar o nosso arquivo `main.py`.

```python
# main.py
import typer

# Cria uma instância da aplicação
app = typer.Typer()

# Cria um comando do CLI
@app.command()
def soma(a: int, b: int):
    print(a + b)

# Cria um segundo comando do CLI
@app.command()
def subtracao(a: int, b: int):
    print(a - b)

# Executa a aplicação
if __name__ == "__main__":
    app()

```

Agora, vamos executar o nosso script com o comando: `python3 src/main.py --help`, para obter a seguinte saída na tela:

```bash
Usage: main.py [OPTIONS] COMMAND [ARGS]...
 Options 
 --install-completion          Install completion for the current shell.
 --show-completion             Show completion for the current shell, to copy it or customize the installation.               
 --help                        Show this message and exit.                                               

 Commands  
  soma
  subtracao    
```

Agora vamos testar nossa aplicação com o comando `soma`:

```bash
python3 src/main.py soma 1 2
```

E posteriormente com o comando:

```bash
python3 src/main.py subtracao 1 2
```

Assim criamos duas funcionalidades para nossa CLI. Agora precisamos compreender a diferença entre parâmetros opcionais e obrigatórios. Quando criamos um parâmetro, ele é obrigatório por padrão. Se quisermos que um parâmetro seja opcional, basta adicionar o valor padrão para ele. Vamos alterar o nosso arquivo `main.py` para adicionar um parâmetro opcional.

Parâmetros que são opcionais devem ter um valor padrão. Por exemplo, se quisermos que o parâmetro `b` seja opcional, basta adicionar um valor padrão para ele. Vamos alterar o nosso arquivo `main.py` para adicionar um parâmetro opcional.

```python
# main.py
import typer

# Cria uma instância da aplicação
app = typer.Typer()

# Cria um comando do CLI
@app.command()
def soma(a: int, b: int = 0):
    print(a + b)

# Cria um segundo comando do CLI
@app.command()
def subtracao(a: int, b: int = 0):
    print(a - b)

# Executa a aplicação
if __name__ == "__main__":
    app()

```

Agora ao executar o comando `python3 src/main.py soma --help`, vamos obter a seguinte saída na tela:

```bash
Usage: main.py soma [OPTIONS] A
 Options 
 --install-completion          Install completion for the current shell.
 --show-completion             Show completion for the current shell, to copy it or customize the installation.               
 --help                        Show this message and exit.                                               

 Arguments 
  a                             [required]
 Options 
  --b INTEGER[default:0]                                                                                          │
  --help Show this message and exit.   
```

Maravilha, estamos avançando com nossa aplicação em CLI. Vamos agora tornar ela mais interativa com o usuário, pedindo entradas para ele, quando ela for executada.

Agora, vamos alterar nosso arquivo `main.py` para que ele peça entradas para o usuário.

```python
# main.py
import typer

# Cria uma instância da aplicação
app = typer.Typer()

# Cria um comando do CLI
@app.command()
def soma(a: int, b: int = 0):
    print(a + b)

# Cria um segundo comando do CLI
@app.command()
def subtracao(a: int, b: int = 0):
    print(a - b)

# Cria um terceiro comando do CLI
@app.command()
def soma_interativa():
    a = typer.prompt("Digite o primeiro número")
    b = typer.prompt("Digite o segundo número")
    print(int(a) + int(b))
    
# Executa a aplicação
if __name__ == "__main__":
    app()

```

Agora pessoal, vamos primeiro ver como ficaram nossos comandos. Vamos executar o comando `python3 src/main.py --help`, para obter a seguinte saída na tela:

```bash
Usage: main.py [OPTIONS] COMMAND [ARGS]...
 Options 
 --install-completion          Install completion for the current shell.
 --show-completion             Show completion for the current shell, to copy it or customize the installation.               
 --help                        Show this message and exit.                                               

 Commands  
  soma
  subtracao
  soma-interativa
```

Agora vamos testar nossa aplicação com o comando `soma-interativa`:

```bash
python3 src/main.py soma-interativa
```

Esse comando vai abrir a interação do sistema com o usuário, permitindo que ele digite os valores para a soma.
Vamos melhorar ainda mais essa experiência, não encerrando o programa quando ele está em execução, vamos perguntar para o usuário se ele deseja sair ou se ele deseja continuar em nossa interação.

```python
# main.py
import typer

# Cria uma instância da aplicação
app = typer.Typer()

# Cria um comando do CLI
@app.command()
def soma(a: int, b: int = 0):
    print(a + b)

# Cria um segundo comando do CLI
@app.command()
def subtracao(a: int, b: int = 0):
    print(a - b)

# Cria um terceiro comando do CLI
@app.command()
def soma_interativa():
    continuar = True
    while continuar:
        a = typer.prompt("Digite o primeiro número")
        b = typer.prompt("Digite o segundo número")
        print(int(a) + int(b))
        continuar = typer.confirm("Deseja continuar?")

# Executa a aplicação
if __name__ == "__main__":
    app()

```

Repare que agora, nossa aplicação não apenas interage com o usuário para que ele possa informar os parâmetros dela, mas também interage com o usuário para que ele possa decidir se deseja continuar ou não com a interação 🍱.

Agora vamos adicionar um conjunto de outras dependências em nossa aplicação para elevar ainda mais a interação com o usuário do sistema.

Vamos adicionar algumas outras funcionalidades no sistema, como barra de carregamento e algumas interações para escolher entre algumas opções pré-definidas para o usuário. Para isso vamos utilizar a biblioteca [`inquirer`](https://python-inquirer.readthedocs.io/en/latest/). Ela foi inspirada em uma biblioteca de mesmo nome para o Node.js, e nos permite criar interações com o usuário de forma fácil e rápida.

Primeiro vamos adicionar essa biblioteca em nosso ambiente virtual e depois vamos atualizar as dependências do nosso projeto. Para isso, vamos executar o seguinte comando:

```bash
pip install inquirer
pip freeze > requirements.txt
```

Agora vamos alterar o nosso arquivo `main.py` para adicionar uma interação para escolher entre algumas opções pré-definidas para o usuário.

```python
# main.py
import typer
import inquirer

# Cria uma instância da aplicação
app = typer.Typer()

# Cria um comando do CLI
@app.command()
def soma(a: int, b: int = 0):
    print(a + b)

# Cria um segundo comando do CLI
@app.command()
def subtracao(a: int, b: int = 0):
    print(a - b)

# Cria um terceiro comando do CLI
@app.command()
def soma_interativa():
    continuar = True
    while continuar:
        a = typer.prompt("Digite o primeiro número")
        b = typer.prompt("Digite o segundo número")
        print(int(a) + int(b))
        continuar = typer.confirm("Deseja continuar?")

# Cria um quarto comando do CLI
@app.command()
def calculadora():
    # realiza lista de perguntas para o usuário
    perguntas = [
        inquirer.List("operacao", message="Qual operação deseja realizar?", choices=["soma", "subtração","multiplicacao","divisao"]),
        inquirer.Text("a", message="Digite o primeiro número"),
        inquirer.Text("b", message="Digite o segundo número")
    ]
    # realiza a leitura das respostas
    respostas = inquirer.prompt(perguntas)
    # apresenta as respostas que o usuário digitou
    print(respostas)
# Executa a aplicação
if __name__ == "__main__":
    app()
```

Ao executar o programa com `python3 src/main.py calculadora`, vamos ver que ele vai apresentar para o usuário uma lista de opções para ele escolher. E depois que ele escolher a opção, ele vai pedir para o usuário digitar os valores para a operação.

```bash
[?] Qual operação deseja realizar?: 
   soma
 > subtração
   multiplicacao
   divisao

[?] Digite o primeiro número: 3
[?] Digite o segundo número: 4
{'operacao': 'subtração', 'a': '3', 'b': '4'}
```

Podemos ver que as respostas do usuário ficam disponíveis em um dicionário. Isso é importante para que possamos utilizar as respostas do usuário para realizar as operações que ele deseja. Agora, além de adicionarmos as operações propriamente ditas, vamos adicionar também a barra de carregamento para o usuário. Para isso, vamos utilizar a [`yaspin`](https://github.com/pavdmyt/yaspin). A biblioteca `yaspin` é uma biblioteca que nos permite criar barras de carregamento de forma fácil e rápida. 

Vamos adicionar ela no nosso ambiente virtual e depois vamos atualizar as dependências do nosso projeto. Para isso, vamos executar o seguinte comando:

```bash
pip install yaspin
pip freeze > requirements.txt
```

Agora vamos alterar o nosso arquivo `main.py` para adicionar uma barra de carregamento para o usuário.

```python
# main.py
import typer
import inquirer
from yaspin import yaspin
import time

# Cria uma instância da aplicação
app = typer.Typer()

# Cria um comando do CLI
@app.command()
def soma(a: int, b: int = 0):
    print(a + b)

# Cria um segundo comando do CLI
@app.command()
def subtracao(a: int, b: int = 0):
    print(a - b)

# Cria um terceiro comando do CLI
@app.command()
def soma_interativa():
    continuar = True
    while continuar:
        a = typer.prompt("Digite o primeiro número")
        b = typer.prompt("Digite o segundo número")
        print(int(a) + int(b))
        continuar = typer.confirm("Deseja continuar?")

# Cria um quarto comando do CLI
@app.command()
def calculadora():
    # realiza lista de perguntas para o usuário
    perguntas = [
        inquirer.List("operacao", message="Qual operação deseja realizar?", choices=["soma", "subtração","multiplicacao","divisao"]),
        inquirer.Text("a", message="Digite o primeiro número"),
        inquirer.Text("b", message="Digite o segundo número")
    ]
    # realiza a leitura das respostas
    respostas = inquirer.prompt(perguntas)
    # chama a funcao que processa a operação e exibe uma spinner para o usuário
    spinner = yaspin(text="Processando...", color="yellow")
    # inicia o spinner
    spinner.start()
    # realiza a operação
    saida = processar(respostas)
    # para o spinner
    spinner.stop()
    # exibe o resultado
    print(saida)

# Função que processa a operação
def processar(dados):
    time.sleep(5)
    operacao = dados["operacao"]
    a = float(dados["a"])
    b = float(dados["b"])
    if operacao == "soma":
        return (a + b)
    elif operacao == "subtração":
        return (a - b)
    elif operacao == "multiplicacao":
        return (a * b)
    elif operacao == "divisao":
        return (a / b)
    
# Executa a aplicação
if __name__ == "__main__":
    app()

```

O resultado da execução do nosso programa (`python3 src/main.py calculadora`) vai ser uma barra de carregamento que vai aparecer para o usuário enquanto o programa está processando a operação que ele escolheu.

```bash
[?] Qual operação deseja realizar?: 
   soma
 > subtração
   multiplicacao
   divisao

[?] Digite o primeiro número: 3
[?] Digite o segundo número: 4
Processando...
-3
```

:::tip[Cuidado com o volume de informação]

<img src="https://media1.tenor.com/m/sgdOFizLVJcAAAAC/mashle-gojo.gif" alt="Gojo Dançando Mashle" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: 24 }} />

Pessoal até aqui, fomos de forma incremental, mas ainda assim não foi pouco conteúdo. É importante que você registre, teste, aplique os conhecimentos que apresentamos até aqui. E se você tiver dúvidas, não hesite em perguntar.

:::