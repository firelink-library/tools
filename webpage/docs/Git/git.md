---
title: Configurando o Git
sidebar_position: 1
slug: /git2
---

# Configuração do Git

Git é um programa de versionamento de arquivos (funciona com todo o tipo de
arquivo, mas é mais poderoso com arquivos de texto) que ao mesmo tempo segue a
filosofia UNIX (tem apenas uma função, executada com maestria) e oferece
ferramentas de versionamento extremamente robustas. Por essas característica,
Git virou o padrão de versionamento de projeto de programação. Ser um
desenvolvedor e não saber usar o Git é a mesma coisa que ser um jogador de
futebol que não sabe calçar as chuteiras; pode até ser que consiga entrar em
campo, mas é provável que passe o jogo todo escorregando.

Sendo assim, vamos aprender a calçar as chuteiras?

<img 
  src="https://i.makeagif.com/media/6-28-2018/YYDpk9.gif"
  alt="Boot process" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '70vh',
    marginRight: 'auto'
  }} 
/>
<br/>

## 1. Instalando o git

Se você está usando o Linux, é bastante provável que já tenha o git instalado.
Caso não tenha, basta instalar utilizando o gerenciador de pacotes:

```bash
sudo apt install git
```

:::tip

A maioria das distribuições de Linux oferecem metapacotes que juntam todas as
ferramentas mais comuns para desenvolvimento de software, bastando um único
comando para instalá-las. No Ubuntu, esse metapacote se chama `base-devel`.

```bash
sudo apt install base-devel
```

:::

Agora que temos uma instalação do git, vamos configurá-lo corretamente?

## 2. Criando uma chave ssh

Desde o começo de 2022, o github não permite mais que você autentique seu
acesso ao repositório para `push` e `pull` utilizando seu usuário e senha. O
motivo disso? Segurança. A maneira obrigatória agora passa a ser utilizando
**criptografia assimétrica**. O que isso significa? Que você precisa configurar
uma chave privada e uma chave pública. A chave pública deve ser registrada no
github.

Para criar a chave, você pode seguir [esse
tutorial](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
oficial do github. No entanto, eu criei um script para que você possa fazer
toda a configuração do git com a chave ssh.

Para usar meu script, clone meu repositório de scripts (aqui tem vários scripts
úteis. Usem sem parcimônia ~e quebrem seu sistema operacional~).

```bash
git clone https://github.com/rmnicola/Scripts.git && cd Scripts
```
Como eu sou ~preguiçoso~ muito organizado, eu criei um script que basicamente
pega todos os scripts existentes nessa pasta de scripts e cria um link
simbólico para que eles fiquem disponíveis em `/usr/bin/`, que é a pasta onde
ficam os arquivos binários executáveis do seu usuário no Linux. Eu fiz isso
pois a partir do momento em que essa configuração é feita, todos os scripts
passam a ser acessíveis de qualquer lugar do sistema, como se fosse um programa
que você instalou (o motivo disso é porque ele **é** um programa que você
instalou).

```bash
sudo ./install.sh
```

Se o output do comando tiver essa carinha:

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

Significa que deu tudo certo.

O primeiro passo é instalar a linguagem `go`. Por quê? Porque eu criei uma
interface amigável que foi feita utilizando uma ferramenta que precisa do go
instalado no seu sistema (`bubblegum`).

Para instalar o `go`, rode:

```bash
go-install
```

Ao final desse comando, você vai ver três linhas que devem ser adicionadas ao
seu `.bashrc`. Adicione elas e rode `source .bashrc` para poder utilizar o go.
Se tudo deu certo, o comando a seguir vai mostrar a versão de `go` instalada no
seu sistema:

```bash
go version
```

Legal, agora podemos instalar o `bubblegum`:

```bash
charm-cli-install
```

Agora, vamos apenas garantir que outras duas ferramentas necessárias para rodar
meus scripts estejam instaladas:

```bash
sudo apt install figlet xclip
```

Pronto! Agora, rode:

```bash
generate-ssh-key
```

E siga as instruções no terminal para gerar sua chave ssh. Sugiro utilizar o
título padrão e não configurar uma senha para poder dar push sem digitar essa
senha toda vez.

Ao final da execução desse comando, você vai ver dois links no seu terminal. O
primeiro deles é o que vai te levar para a página onde você deve adicionar a
sua chave SSH no github. Segue o [link](https://github.com/settings/keys).

Nessa página, você deve clicar em **New SSH key**. Isso vai te levar para uma
página onde você deve definir um título e colocar a sua chave pública. Meu
script foi feito com carinho, então assim que você executa ele, a sua chave
pública fica disponível no seu `clipboard` para colar a qualquer momento
utilizando **CTRL V**. De nada!

Sugiro criar duas chaves, uma para **autenticação** e outra para
**assinatura**. A de assinatura não é exatamente necessária, mas sem ela seus
commits não vão ter o check verdinho ao lado.

Quer testar se deu certo? Rode o seguinte comando:

```bash
ssh git@github.com
```

Legal, agora você tem uma chave ssh configurada e cadastrada no Github. O
próximo passo é configurar o git.

## 3. Configurando o git

### 3.1. Usando meu script

Essa vai ser rápida. Rode:

```bash
git-configure
```

E siga as instruções que vão aparecer no seu terminal.

Quer fazer tudo na mão? Beleza, siga o tutorial que vem a seguir.

### 3.2. Na mão

#### 3.2.1. Adicionando seu nome e email

O git é uma ferramenta que pode ser usada para ~atribuir culpa~ registrar os
responsáveis por cada parte do código do projeto. Sendo assim, você precisa
registrar ao menos seu nome completo e email antes de conseguir fazer um
`commit`.

```bash
git config --global user.name "Seu Nome Aqui"
git config --global user.email "seu.email@aqui"
```

Sempre que você usar o comando `git commit`, o git vai usar um editor para que
você possa escrever sua mensagem de commit. Caso você não mexa nessa
configuração, o padrão do git será o vim. Se você nuna usou o vim na vida, a
experiência de dar um commit e ser jogado dentro do editor pode ser um pouco
traumática.

<img 
  src="https://preview.redd.it/b5bt8nv08qm61.jpg?width=640&crop=smart&auto=webp&s=38e18aba6ce0a20846a573a2ac033b54705f92c7"
  alt="Boot process" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>
<br/>

Para configurar seu editor padrão do vim, use:

```bash
git config --global core.editor "code"
```

O comando acima configura como editor padrão o **vscode**.

## 4. Tutorial Git

Para saber mais sobre git, leia [esse livro
gratuito](https://git-scm.com/book/en/v2)

