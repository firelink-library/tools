---
title: Github
slug: /github
sidebar_position: 2
---

# Entendendo o Github

Por enquanto este material vai focar na utilização do github actions, tomando
como exemplo a criação de um *workflow* para hospedar automaticamente uma
documentação gerada pelo *docusaurus* no *Github pages*. Em breve haverá mais
material aqui.

## 1. Utilizando o Github Actions

O GitHub Actions é uma ferramenta de automação que permite configurar fluxos de
trabalho (workflows) diretamente no seu repositório do Github. A utilidade de
criar esses fluxos de trabalho é que eles podem ser executados pelas máquinas
virtuais do Github de acordo com os gatilhos definidos por você em um arquivo
de configuração. Isso significa que você pode automatizar tarefas para rodar de
forma independente do seu hardware e até mesmo simulando diversos sistemas
operacionais e configurações. Com isso, podemos criar um mecanismo para
realizar testes automatizados, builds, deployments. Esse tipo de esteira de
automação é o que permite a implementação de CI/CD em times de desenvolvimento.
Sendo assim, é bem útil para um desenvolvedor aprender ao menos o básico do
Github Actions.

Em nosso módulo, vamos utilizar o Github Actions como uma forma conveniente de
automatizar o deploy de nossa página de documentação (docusaurus) e alguns de
nossos testes. Portanto, a seguir criaremos um workflow simples para
exemplificar o que é possível fazer com o Actions.

## 1. Criando o primeiro workflow

Para criar um workflow novo, basta criar a pasta `.github/workflows` na raíz do
seu repositório.

```bash
mkdir -p .github/workflows
```

A seguir, vamos criar um arquivo contendo nossa workflow de teste. O arquivo de
configuração de workflows do actions é o `yaml`. Ele é um formato de arquivo de
texto puro estruturado de forma hierarquica. Diferente do `xml`, o `yaml` é um
formato de arquivo menos verboso e, portanto, mais fácil de ser lido por um ser
humano. Para saber mais sobre esse formato, acesse [esse
link](https://spacelift.io/blog/yaml). Crie um arquivo chamado `teste.yaml` e
vamos adicionar o seguinte conteúdo:

```yaml showLineNumbers title="teste.yaml"
name: Testa o github actions

on: [push]

jobs:
  teste:
    runs-on: ubuntu-latest

    steps:
    - name: Roda um script simples que exibe "Hello, world!"
      run: echo Hello, world!
```

Vamos dissecar esse arquivo para entender o que ele está fazendo.

O trecho:

```yaml
on: [push]
```

Indica que o workflow descrito neste arquivo roda sempre que há uma ação de
`push` no repositório. Para entender melhor quais ações podem ser usadas como
gatilhos para execução de workflows, você pode acessar a [documentação oficial
do github
    actions](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

O que vem após a chave `jobs` são as diferentes **tarefas** descritas no
workflow. Note que a tarefa que criamos se chama `teste`. Tarefas são alocadas
para um worker e podem ter diversos passos definidos (chave `steps`). Esses
passos são executados em sequência e dividem o ambiente de execução.

Por fim, o nosso passo usa a chave `run` para especificar um comando em `bash`
a ser rodado. Esse comando pode ser multi-linhas ou mesmo um script
(certifique-se de que baixou o arquivo do script antes de tentar executá-lo no
ambiente do github actions)

Ou seja, esse arquivo define um workflow chamado `Testa o github actions`, que
contem um job chamado `teste`, que roda em Ubuntu e executa apenas um passo que
roda o comando `echo Hello, world!`. Esse workflow é acionado sempre que há um
evento de `push` para o repositório, independente de qual branch.

Para exemplificar os workflows desse tutorial, criei um [repositório de
exemplo](https://github.com/rmnicola/actions-examples) para que seja possível
ver os seus efeitos na prática. A imagem a seguir demonstra a execução do
workflow `Testa o github actions`.

<img 
  src="img/workflow-run-1.png"
  alt="Workflow run 1" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '70vh',
    marginRight: 'auto'
  }} 
/>

Legal, mas esse ainda é um uso muito limitado do Github Actions. A seguir,
vamos ver como usar **ações prontas**

## 2. Utilizando ações prontas no seu workflow

Para que seja mais fácil compor ações mais complexas sem precisar reinventar a
roda toda vez, o github definiu um padrão para ações que podem ser
compartilhadas. Essas ações podem ser encontradas no [Github
Marketplace](https://github.com/marketplace?type=actions). Há uma infinidade de
ações lá, a maioria criada e publicada por outros usuários. No entanto, a ação
que vamos utilizar a seguir foi publicada pelo proprio Github. Essa ação é a
[ação de checkout de
repositório](https://github.com/marketplace/actions/checkout).

A ação de checkout de repositório serve para que o ambiente de execução das
tarefas do seu workflow tenha acesso aos arquivos do seu repositório. De forma
resumida, é apenas uma ação que faz `clone` do seu repositório, entra na sua
pasta raíz e configura as chaves necessárias para ter o acesso adequado.
Trata-se de um processo sem grandes dificuldades, mas que pode ser tedioso de
configurar e debugar manualmente. É exatamente para esse tipo de tarefa que o
sistema de ações prontas brilha. Vamos construir um exemplo simples que use
essa tarefa:

Primeiro vamos criar um arquivo com um texto para exibirmos em nossa tarefa.
Para isso, crie um arquivo chamado `texto-muito-importante.txt` com o seguinte
conteúdo:

```txt showLineNumbers title="texto-muito-importante.txt"
Killua > Gon
```

Legal, agora vamos criar uma nova workflow chamada `confirma-verdades.yaml`.
Lembre-se que esse arquivo deve estar no diretório `.github/workflows`. O
conteúdo do arquivo deve ser:

```yaml showLineNumbers title=".github/workflows/confirma-verdades.yaml"
name: Confirma verdades absolutas

on: [push]

jobs:
  verdades:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v4

    - name: Exibe conteúdo de arquivo txt
      run: cat texto-muito-importante.txt
```

Note que agora temos duas etapas na nossa tarefa `verdades`. Primeiro fazemos o
`checkout` no repositório e depois exibimos o conteúdo do arquivo `.txt`.

O resultado do segundo workflow pode ser visto abaixo:

<img 
  src="img/workflow-run-2.png"
  alt="Workflow run 2" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '70vh',
    marginRight: 'auto'
  }} 
/>

Se você está seguindo esse tutorial do jeito certo (fazendo junto), vai notar
que dessa vez tivemos dois workflows que executaram em paralelo. De fato, seu
repositório pode ter inúmeros workflows que rodam no mesmo ou em diferentes
gatilhos, criando uma granularidade muito grande para automatizar as ações do
seu projeto.

## 3. Deploy da documentação para o github pages

Agora vamos um passo além. O workflow que vou apresentar agora é bem mais
complexo que os dois primeiros que fizemos, porém utiliza apenas os conceitos
que foram apresentados. Vamos lá?

Antes de mais nada, habilite o seu repositório para a utilização de github
pages. Para fazer isso, entre na página do seu repo e siga: Settings > Pages >
Source > Github Actions. A imagem abaixo demonstra o que você deve ver se
configurou o repositório corretamente para a próxima etapa:

<img 
  src="img/config-pages.png"
  alt="Config github pages" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '70vh',
    marginRight: 'auto'
  }} 
/>

Ok. Agora vamos detalhar a primeira workflow que vamos fazer. Ela vai se chamar
`Deploy to Github Pages` e vai contar com duas tarefas distintas:

1. A tarefa `build`, que vai compilar e configurar toda a nossa página do
   docusaurus para prepará-la para o upload para o Github Pages. As etapas que
   ela vai executar são:

   * Checkout no repo
   * Setup do node v18
   * Instalação de dependencias npm
   * Build do docusaurus
   * Configura o pages
   * Comprime a pasta build e faz o upload do artefato

2. A tarefa `deploy` vai pegar o artefato carregado e fazer o deploy dele no
   Github Pages.

O arquivo completo pode ser visto a seguir:

```yaml showLineNumbers title=".github/workflows/deploy.yaml"
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
    
permissions:
  contents: write

jobs:
  build:
    name: Build and upload artifact
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
        working-directory: ./Material
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies
        run: npm ci
      - name: Build website
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v4
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./Material/build

  deploy:
    name: Deploy to GitHub Pages
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

Note que essa workflow restringe o gatilho para apenas executar quando há
`push` na branch `main`. Fazemos isso pois não queremos transformar o conteúdo
de outras branches em uma página no Github Pages.

Legal, acabou né? Não!!! Acabou nada! Você é o tipo de pessoa que faz push
direto para produção? Pois é quase isso que estamos fazendo agora. Ao criar
apenas essa workflow, estamos confiando (sem testar) que a página do docusaurus
está pronta para ir ao ar. Vamos criar uma segunda workflow que testa toda a
tarefa de `build`? Melhor ainda: vamos fazer com que essa workflow rode sempre
que há um `pull-request` que envolve a branch `main`. Assim, vamos conseguir
verificar direto em um `pull-request` se existe algum problema com o processo
de `build` da nossa página do docusaurus. Perfeito, né? Tá aqui o arquivo
`yaml` dessa workflow:

```yaml showLineNumbers title=".github/workflows/test-deploy.yaml"
name: Test deployment

on:
  pull_request:
    branches:
      - main

jobs:
  test-build:
    name: Test build and artifact upload
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
        working-directory: ./Material
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: actions/setup-node@v4
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci
      - name: Test build website
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v4
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./Material/build
```

Pronto! A figura abaixo mostra como funciona esse teste em um caso real: ao
criar esse material, o docusaurus compilou corretamente localmente mas falhou
quando fiz o PR para a `main`. Eu consegui verificar pelo `log` do workflow
qual foi o erro e criar um novo `commit` na PR corrigindo o erro. Assim que o
segundo teste foi bem sucedido, dei merge na `main` e tudo correu bem sem
quebrar a "prod". É assim que desenvolvedores profissionais *deveriam*
trabalhar.

<img 
  src="img/pr-fix.png"
  alt="Testes automatizando salvando prod" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '70vh',
    marginRight: 'auto'
  }} 
/>

