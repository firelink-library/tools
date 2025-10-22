---
title: Instalando o ROS
sidebar_position: 1
slug: /ros-install
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Instalação do ROS

:::warning Aviso

A instalação descrita neste artigo está **desatualizada**. Por favor, siga 
um dos tutoriais abaixo:

* [ROS Jazzy Jalisco](https://docs.ros.org/en/jazzy/Installation.html) é a última versão que utilizamos em um módulo do 
Inteli. Ele é compatível com o **Ubuntu 24.04**.
* [ROS Kilted Kaiju](https://docs.ros.org/en/kilted/Installation.html) é a
versão mais nova disponível. Compatível com **Ubuntu 24.04**. Pode ser que tenha
problemas de compatibilidade com o *Turtlebot* ou o *Unitree GO2*. Se for
instalar esse, me conte se tiver algum problema.
* [ROS Rolling Ridley](https://docs.ros.org/en/rolling/Installation.html) é a versão *rolling release* do ROS. Se você não se
importa com instabilidade e não quer mais ter que atualizar versões de ROS, use
esse.

:::

Para instalar o ROS, podemos seguir de duas formas distintas:

1. A forma fácil, usando meu script de instalação automática; ou
2. A forma convencional, configurando os repositórios apt e instalando tudo na
   mão.

## 1. Script de instalação automática

Antes de mais nada, garanta que o git está instalado com:
```bash
sudo apt install git -y
```

Em meu repositório eu guardo alguns scripts úteis para que eu possa configurar
meu sistema rapidamente (vou criar uma seção mostrando **o que** exatamente eu
costumo configurar). A boa notícia é que uma das coisas para as quais eu criei
um script é para a instalação do ROS. Portanto, podemos seguir apenas usando
esse script.

Para isso, clone o meu repositório:

```bash
git clone https://github.com/rmnicola/Scripts.git
cd Scripts
```

A estrutura do diretório é essa:

```bash
.
├── 01Basics
│   ├── charm-cli-install.sh
│   ├── dotfiles-link.sh
│   ├── flatpak-install.sh
│   ├── go-install.sh
│   ├── starship-install.sh
│   └── zsh-install.sh
├── 02Gnome
│   ├── fonts-install.sh
│   ├── gnome-pull.sh
│   └── gnome-push.sh
├── 03Dev
│   ├── generate-ssh-key.sh
│   ├── git-configure.sh
│   ├── node-install.sh
│   └── rust-install.sh
├── 04Arch
│   └── ilovecandy.sh
├── 05Ubuntu
│   ├── neovim-install.sh
│   ├── ros-install.sh
│   └── ros-start.sh
├── 06Peripherals
│   ├── configure-bt-autosuspend.sh
│   └── logiops-install.sh
├── install.sh
└── README.md
```

Note que eu dividi os scripts em seções. Na seção de Ubuntu é onde guardo dois
scripts que uso para o ROS. Mas **CALMA**, antes de usar os scripts de ROS você
vai precisar usar alguns outros scripts. Antes de mais nada, vamos instalar os
scripts para que fique mais fácil rodar eles. Para isso, garanta que você está
dentro do diretório `Scripts` e rode:

```bash
sudo ./install.sh
```

O output desse script deve ser algo como:

```bash
Symlink created for charm-cli-install
Symlink created for dotfiles-link
Symlink created for flatpak-install
Symlink created for go-install
Symlink created for starship-install
Symlink created for zsh-install
Symlink created for fonts-install
Symlink created for gnome-pull
Symlink created for gnome-push
Symlink created for generate-ssh-key
Symlink created for git-configure
Symlink created for node-install
Symlink created for rust-install
Symlink created for ilovecandy
Symlink created for neovim-install
Symlink created for ros-install
Symlink created for ros-start
Symlink created for configure-bt-autosuspend
Symlink created for logiops-install
```

Agora temos os scripts todos instalados. Quais vamos precisar usar? Em ordem de
uso:

1. go-install
2. charm-cli-install
3. instalação do figlet
4. instalação do ROS

Portanto, instale o golang com:

```bash
sudo go-install
```

Ao final da instalação, modifique seu `bashrc`, adicionando o seguinte:

:::tip DICA

O que é o **bashrc**?

Na origem dos computadores, a primeira forma de criar **sistemas
multiusuários** foi o uso de **terminais**. Neles, era possível que vários
usuários enfileirassem comandos para execução no mainframe.

Hoje em dia não precisamos mais utilizar teleterminais para interagir com
nossos sistemas, mas uma herança dessa época é o uso de **emuladores de
terminal**. Eles são basicamente os programas que usamos em nossas interfaces
gráficas para interagir com o sistema por linha de comando.

Onde eu quero chegar com isso? Bom, esses emuladores de terminal precisam
utilizar alguma **linguagem** para entender os comandos do usuário. A linguagem
mais comum para esses comandos se chama Bourne Again SHell, ou bash para os
íntimos. Isso significa que sempre que você abre um terminal, você está
inicializando uma sessão interativa com uma linguagem scriptada chamada bash.

O que isso tem a ver com o `bashrc`? Simples; toda vez que essa sessão
interativa é inicializada, o sistema busca por um arquivo especial de
**configuração** para essa sessão. Esse arquivo é... o `bashrc`.

O que estamos fazendo agora? Configurando no `bashrc` para que ele identifique
a instalação de golang e disponibilize para nós comandos como o `go install`.

Onde fica o `bashrc`? Na sua **HOME**. É um arquivo **escondido** (o caminho
real é `.bashrc`), portanto utilize `ls -a` para conseguir enxergá-lo.

:::

```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

Onde fica o `bashrc`? No seu home. Utilize o caminho `~/.bashrc`. Caso você
utilize zsh, confio que já está em um nível para saber onde está seu arquivo
`zshrc`.

Após isso, vamos instalar o charm cli com:

```bash
charm-cli-install
```

Vamos instalar o figlet com:

```bash
sudo apt install figlet
```

E, por fim, podemos instalar o ROS com:

```bash
ros-install
```

Você vai ver um menu para selecionar o que quer configurar do ROS. Caso não
saiba o que são as opções, o mais provável é que você queira **todas**. Utilize
as setas do teclado para navegar nas opções e o espaço para selecionar cada
opção.

Após a instalação, não se esqueça de adicionar `source
/opt/ros/humble/setup.xxx` ao arquivo de configuração do seu shell,
substituindo o `xxx` pela extensão adequada. (mais comuns bash e zsh). Veja
abaixo:

<Tabs defaultValue="bash" values={[
        {label: 'Bash', value: 'bash'},
        {label: 'Zsh', value: 'zsh'},
        {label: 'Zsh com a minha config.', value: 'zsh-meu'},
  ]}>

<TabItem value="bash">

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```

</TabItem>

<TabItem value="zsh">

```bash
echo "source /opt/ros/humble/setup.zsh" >> ~/.zshrc
```

</TabItem>

<TabItem value="zsh-meu">

```bash
echo "source /opt/ros/humble/setup.zsh" >> '$ZODTDIR'/.zshrc
```

</TabItem>
</Tabs>

## 2. Na raça

:::warning

Esse vídeo está desatualizado para o nosso módulo, mas os conceitos que estão
apresentado ali ainda são validos. O que mudou? Não utilizamos mais WSL ~graças
a Deus~. O que **não** mudou? O procedimento de instalação do ROS. O que **pode
ser** que tenha mudado? Os exatos comandos utilizados. Para encontrar as
versões mais atualizadas, siga esse
[guia](https://docs.ros.org/en/humble/Installation.html)

:::

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/Dt1x4NBPp-Y" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>

Para instalar o ROS, precisamos adicionar novos repositórios ao apt, pois o ROS
não se encontra nos repositórios padrão do Ubuntu. Para isso começaremos
garantindo que o repositório `universe` está habilitado. Rode:

```bash
sudo apt-add-repository universe
```

A seguir, precisamos baixar uma chave GPG e adicioná-la ao keyring do sistema
para poder validar o repositório que vamos adicionar. Rode:
```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

Agora precisamos adicionar o repositório à lista de repositórios. Use:
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

Como fizemos alterações nos repositórios do apt, precisamos atualizar seu banco
de dados novamente. Rode:

```bash
sudo apt update
```

Pronto! Agora estamos finalmente prontos para instalar a nossa distribuição de
ROS. Para facilitar nossa vida, vamos escolher a versão do pacote mais
completa, assim não precisaremos nos preocupar se os exemplos e pacotes que
vamos precisar já estarão instalados ou não. Rode:

```bash
sudo apt install ros-humble-desktop
```

Essa instalação vai demorar alguns minutos, então tenha paciência =)

Falta apenas uma coisa para termos o poder do ROS em nossas mãos: por padrão, o
ROS não adiciona automaticamente todos os executáveis e variáveis de ambiente
ao nosso sistema, mas existe um script que faz todo esse setup para nós. Como
ninguém tem tempo de ficar dando source nesse script toda vez, rodem esse
comando para garantir que tudo vai estar configurado sempre que você abrir o
terminal do WSL:

:::caution Aviso
 
O comando abaixo vai reconfigurar seu bashrc para que, da proxima vez, ele
consiga identificar os comandos do ROS. Caso não queira reiniciar o terminal,
rode:

```bash
source ~./bashrc
```
 
:::

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```
## 3. Testando a instalação

Perfeito! Agora estamos prontos para trabalhar com o ROS2 Humble. Vamos testar?

Abra dois terminais e, para cada um deles vamos rodar um comando. Para o
terminal 1:

```bash
ros2 run demo_nodes_cpp talker
```

Para o terminal 2:
```bash
ros2 run demo_nodes_cpp listener
```

Se tudo deu certo, você acabou de ver dois processos totalmente independentes
conversando através da interface de comunicação do ROS. Legal, né? Para fechar
as instruções necessárias, vamos apenas aprender a rodar nosso exemplo.
