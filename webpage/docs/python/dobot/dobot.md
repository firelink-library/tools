---
title: Dobot
sidebar_position: 1
slug: /dobot
---

Pessoal esse material traz um pouco da utilização do Robô Magician Dobot Lite com sua interface em Python. Não necessariamente sua interface, pois utilizamos aqui uma biblioteca de terceiros, mas com o mesmo princípio 🤖!

:::info[Demanda do Robô para Continuar a Desenvolver]

<img src="https://64.media.tumblr.com/89b73637c1c5a5741fb4594214334d6d/4fdec4ce2e98de01-ad/s1280x1920/82fe7bb633bcc2f7cc86c6d9e514eec037657266.gif" alt="Atenção para necessidade do robô" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: 24 }} />

Pessoal a partir daqui os códigos pode ser escritos, mas façam a validação deles utilizando o robô.

:::

A partir deste momento vamos avaliar algumas formas de realizar a comunicação com o robô. É possível realizar a comunicação com o robô utilizando o software DobotStudio, mas também é possível realizar a comunicação com o robô utilizando a biblioteca [`pydobot`](https://github.com/luismesas/pydobot). Vamos avaliar como podemos realizar a comunicação com o robô utilizando a biblioteca pydobot.

Primeiro vamos adicionar a biblioteca *pydobot* no nosso ambiente virtual e depois vamos atualizar as dependências do nosso projeto. Para isso, vamos executar o seguinte comando:

```sh
# Criando o ambiente virtual 
python -m venv venv
# Ativando o ambiente virtual - aqui comando para Windows
\venv\Scripts\activate
# Instalando o pydobot
pip install pydobot
# Para construirmos nossa CLI com mais interatividade
pip install inquirer
# Criando um arquivo com os requisitos
pip freeze > requirements.txt
```

Legal, agora estamos com nossa aplicação pronta para conectar ao robô!

```py
# robo.py

# Traz a ferramenta serial para apresentar quais portas estão disponíveis
from serial.tools import list_ports
import inquirer
import pydobot

# Listas as portas seriais disponíveis
available_ports = list_ports.comports()


# Pede para o usuário escolher uma das portas disponíveis
porta_escolhida = inquirer.prompt([
    inquirer.List("porta", message="Escolha a porta serial", choices=[x.device for x in available_ports])
])["porta"]

print('Porta escolhida:', porta_escolhida)

```

O que aconteceu neste código? Nós utilizamos o `PySerial`, dependência do pyDobot - já vem junto dele quando instalamos a biblioteca para listas as portas seriais disponíveis no nosso sistema. Aqui o [`inquirer`](https://pypi.org/project/inquirer/) é utilizado para trazer uma interface mais amigável com as opções do terminal. Vamos efetivamente colocar nosso robô se comunicando com o programa. 

> ATENÇÃO: Acho importante lembrar, é necessário que o robô esteja ligado e conectado ao computador aqui.

```py
# robo.py

# Traz a ferramenta serial para apresentar quais portas estão disponíveis
from serial.tools import list_ports
import inquirer
import pydobot

# Listas as portas seriais disponíveis
available_ports = list_ports.comports()


# Pede para o usuário escolher uma das portas disponíveis
porta_escolhida = inquirer.prompt([
    inquirer.List("porta", message="Escolha a porta serial", choices=[x.device for x in available_ports])
])["porta"]

# Cria uma instância do robô
robo = pydobot.Dobot(port=porta_escolhida, verbose=False)

# Vamos adicionar nossa lógica aqui!

# Fecha a conexão com o robô
robo.close()
```

O que aconteceu aqui foi utilizar a porta escolhida para realizar a comunicação com o robô. O programa até o momento não faz nenhuma ação diferente de abrir e fechar a conexão com o robô. Mas isso é importante para que possamos saber que a comunicação com o robô está funcionando. O parâmetro verbose é utilizado para que possamos ver as mensagens que estão sendo trocadas entre o programa e o robô. Isso é importante para que possamos saber se a comunicação com o robô está funcionando.

:::danger[Possíveis problemas]

Ocorreu uma vez que a biblioteca `pydobot` não estava funcionando quando baixada pelo pip. A forma de utilizar ela é baixar ela localmente no projeto e incluir ela no repositório.
Para isso, vamos baixar a biblioteca pydobot no nosso ambiente virtual. Para isso, vamos executar o seguinte comando:

```sh
python -m pip install git+https://github.com/luismesas/pydobot.git
```

Ainda execute o comando de instalação pelo pip, para trazer as dependências necessárias para a biblioteca `pydobot`.

Outro problema que aconteceu foi a biblioteca `serial` ter sido instalada no lugar da `PySerial`. Elas não trazem a mesma interface. Neste caso, verificar o que está instalado no sistema:

```sh
python -m pip freeze
```

Se a dependência `serial` estiver listada, remover ela e a `pyserial` para depois realizar a instalação novamente:

```sh
python -m pip uninstall serial
python -m pip uninstall pyserial
python -m pip install pyserial
```

Por fim, um outro problema que aconteceu foi quando utilizando o sistema no Linux, o usuário não estava autorizado a utilizar a porta serial. Neste caso, verificar este post [aqui](https://askubuntu.com/questions/112568/how-do-i-allow-a-non-default-user-to-use-serial-device-ttyusb0). Em geral, este cara deve resolver:

```sh
sudo usermod -a -G dialout $USER
```

:::

Agora vamos pegar a posição atual do robô. Vamos alterar o arquivo robo.py.

```py
# robo.py

# Traz a ferramenta serial para apresentar quais portas estão disponíveis
from serial.tools import list_ports
import inquirer
import pydobot

# Listas as portas seriais disponíveis
available_ports = list_ports.comports()


# Pede para o usuário escolher uma das portas disponíveis
porta_escolhida = inquirer.prompt([
    inquirer.List("porta", message="Escolha a porta serial", choices=[x.device for x in available_ports])
])["porta"]

# Cria uma instância do robô
robo = pydobot.Dobot(port=porta_escolhida, verbose=False)

# Pega a posição atual do robô
posicao_atual = robo.pose()
print(f"Posição atual: {posicao_atual}")

# Fecha a conexão com o robô
robo.close()
```

A posição atual do robô é uma tupla com as informações de:

- x: posição em x em relação a base do robô;
- y: posição em y em relação a base do robô;
- z: posição em z em relação a base do robô;
- r: rotação da ferramenta do robô;
- j1: rotação da junta j1 do robô;
- j2: rotação da junta j2 do robô;
- j3: rotação da junta j3 do robô;
- j4: rotação da junta j4 do robô.


Agora vamos trabalhar na movimentação do robô. Sem definirmos aceleração e velocidade, o robô vai se mover com os parâmetros previamente configurados. Vamos alterar o arquivo robo.py.

```py
# robo.py

# Traz a ferramenta serial para apresentar quais portas estão disponíveis
from serial.tools import list_ports
import inquirer
import pydobot

# Listas as portas seriais disponíveis
available_ports = list_ports.comports()

# Pede para o usuário escolher uma das portas disponíveis
porta_escolhida = inquirer.prompt([
    inquirer.List("porta", message="Escolha a porta serial", choices=[x.device for x in available_ports])
])["porta"]

# Cria uma instância do robô
robo = pydobot.Dobot(port=porta_escolhida, verbose=False)

# Define a velocidade e a aceleracao do robô
robo.speed(30, 30)

# Move o robô para a posição (200, 0, 0)
robo.move_to(200, 0, 0, 0, wait=True)

# Move o robô para a posição (200, 200, 0)
robo.move_to(200, 200, 0, 0, wait=True)

# Move o robô para a posição (0, 200, 0)
robo.move_to(0, 200, 0, 0, wait=True)

# Pega a posição atual do robô
posicao_atual = robo.pose()
print(f"Posição atual: {posicao_atual}")

# Fecha a conexão com o robô
robo.close()

```

O método move_to move o robô para a posição desejada. O parâmetro wait é utilizado para que o programa espere o robô chegar na posição desejada antes de continuar a execução. Isso é importante para que possamos saber que o robô chegou na posição desejada antes de continuar a execução do programa.

Agora vamos adicionar a funcionalidade de pegar e soltar objetos. Vamos alterar o arquivo robo.py.

```py
# robo.py

# Traz a ferramenta serial para apresentar quais portas estão disponíveis
from serial.tools import list_ports
import inquirer
import pydobot

# Listas as portas seriais disponíveis
available_ports = list_ports.comports()


# Pede para o usuário escolher uma das portas disponíveis
porta_escolhida = inquirer.prompt([
    inquirer.List("porta", message="Escolha a porta serial", choices=[x.device for x in available_ports])
])["porta"]

# Cria uma instância do robô
robo = pydobot.Dobot(port=porta_escolhida, verbose=False)

# Define a velocidade e a aceleracao do robô
robo.speed(30, 30)

# Move o robô para a posição (200, 0, 0)
robo.move_to(200, 0, 0, 0, wait=True)

# Inicializa o efetuador do robô
robo.suck(True)
# Adiciona um delay para o robô efetuar a operação
robo.wait(200)

# Move o robô para a posição (200, 200, 0)
robo.move_to(200, 200, 0, 0, wait=True)

# Move o robô para a posição (0, 200, 0)
robo.move_to(0, 200, 0, 0, wait=True)

# Inicializa o efetuador do robô
robo.suck(False)
# Adiciona um delay para o robô efetuar a operação
robo.wait(200)

# Pega a posição atual do robô
posicao_atual = robo.pose()
print(f"Posição atual: {posicao_atual}")

# Fecha a conexão com o robô
robo.close()

```

Agora estamos com os elementos principais para construir nossa CLI e comunicar com o robô. Sugiro fortemente continuar implementando mais funcionalidades para o sistema, como carregar lista de pontos, gravar pontos atuais e o que mais sua imaginação trouxer ✌️🦾🤖.

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSEPWPZGpShg_5c3ao3lGpOSOmVZwfhDkkjLg&s" style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: 24 }} />