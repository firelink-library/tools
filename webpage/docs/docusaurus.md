---
title: Docusaurus
sidebar_position: 4
slug: /docusaurus
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Setup docusaurus V3

O [**docusaurus**](https://docusaurus.io/) é uma ferramenta capaz de gerar sites
estáticos a partir de arquivos `mdx` ou `jsx`. O site criado é perfeito para
fazer documentações completas e fáceis de navegar. Nesta seção, apresentaremos
de forma breve o procedimento de setup da sua página utilizando o docusaurus.

Neste tutorial, iremos configurar o projeto padrão do docusaurus e fazer
algumas alterações para que a página gerada seja **apenas** uma documentação. O
que **não** faremos: configurar o deploy automático do docusaurus no Github
Pages. Isso será mostrado em outra seção deste material. Nesta seção,
trabalharemos apenas com o docusaurus em um host local.

Note que utilizaremos uma estrutura de monorepo para o nosso repositório, o que
significa que o código-fonte e a estrutura da documentação ficarão no mesmo
repositório. Sendo assim, teremos a seguinte estrutura no diretório do
repositório:

```bash
repositorio-do-projeto
├── src # Diretório onde se encontra o código fonte do projeto
│   ├── modulo-a # Sugere-se a divisão do projeto em módulos
│   └── modulo-b
├── docs # Raíz do docusaurus
│   ├── docs # Aqui ficam os seus arquivos .md
│   ├── src
│   ├── statis # imagens/videos/assets utilizados na documentação
│   └── package.json # Dependências do docusaurus
├── media # Imagens e vídeos utilizados para fins de divulgação/apresentação
│   ├── apresentacao-final.mp4
│   └── foto-grupo-apresentacao-final.jpeg
├── README.md  # Aqui é a capa do seu projeto. Seguir padrão institucional
└── LICENSE # Arquivo da licença

```

## 1. Instalando e criando o esqueleto do projeto

Antes de mais nada, vamos criar um projeto-esqueleto utilizando o formato
padrão oferecido pelo docusaurus. Para isso, rode:

```bash
npx create-docusaurus@latest docs classic
```

Note que o nome `docs` pode ser substituído para qualquer nome desejado. No
entanto, o padrão de nosso repositório e das entregas de artefatos requer que o
nome do diretório onde ficará a página de documentação do seu projeto se chame
`docs`.

Para rodar o docusaurus, navegue até a pasta raíz do docusaurus com:

```bash
cd docs
```

E, a seguir, rode:

```bash
npm start
```

Esse comando irá inicializar a versão local da sua documentação. Sugere-se
fortemente o teste local de toda a documentação antes do deploy usando o github
actions. Por padrão, o Docusaurus irá utilizar a porta `3000`. Sendo assim, será
possível acessar a página local em: http://localhost:3000.

## 2. Eliminando a página inicial e a seção de blog

Para o modelo do repositório deste módulo, não é necessário manter a página
inicial e a seção de blog que vem junto com o template padrão do docusaurus.
Podemos, portanto, eliminá-los e criar uma página mais enxuta (anti-bloat gang)

### 2.1. Eliminando a seção de blog

Para eliminar a seção de blog, basta realizar três alterações no arquivo
`docusaurus.config.js`, localizado na raíz do seu projeto docusaurus. Essas
alterações são:

**Colocar `blog: false,` na chave `presets`**

<Tabs>
  <TabItem value="antes" label="Antes" default>
  ```js showLineNumbers title="docusaurus.config.js"
  ...
  presets: [
    [
      'classic',
      /** @type {import('@docusaurus/preset-classic').Options} */
      ({
        docs: {
          sidebarPath: './sidebars.js',
          // Please change this to your repo.
          // Remove this to remove the "edit this page" links.
          editUrl:
            'https://github.com/facebook/...',
        },
        // highlight-start
        blog: {
          showReadingTime: true,
          // Please change this to your repo.
          // Remove this to remove the "edit this page" links.
          editUrl:
            'https://github.com/facebook/...',
        },
        // highlight-end
        theme: {
          customCss: './src/css/custom.css',
        },
      }),
    ],
  ],
  ...
  ```


  </TabItem>
  <TabItem value="depois" label="Depois">
  ```js showLineNumbers title="docusaurus.config.js"
  ...
  presets: [
    [
      'classic',
      /** @type {import('@docusaurus/preset-classic').Options} */
      ({
        docs: {
          sidebarPath: './sidebars.js',
          // Please change this to your repo.
          // Remove this to remove the "edit this page" links.
          editUrl:
            'https://github.com/facebook/...',
        },
        // highlight-start
        blog: false,
        // highlight-end
        theme: {
          customCss: './src/css/custom.css',
        },
      }),
    ],
  ],
  ...
  ```
  </TabItem>
</Tabs>

**Remover o atalho para Blog na chave `themeconfig`**

<Tabs>
  <TabItem value="antes" label="Antes" default>
  ```js showLineNumbers title="docusaurus.config.js"
  ...
  themeConfig:
    /** @type {import('@docusaurus/preset-classic').ThemeConfig} */
    ({
      // Replace with your project's social card
      image: 'img/docusaurus-social-card.jpg',
      navbar: {
        title: 'My Site',
        logo: {
          alt: 'My Site Logo',
          src: 'img/logo.svg',
        },
        items: [
          {
            type: 'docSidebar',
            sidebarId: 'tutorialSidebar',
            position: 'left',
            label: 'Tutorial',
          },
          // highlight-start
          {to: '/blog', label: 'Blog', position: 'left'},
          // highlight-end
          {
            href: 'https://github.com/facebook/docusaurus',
            label: 'GitHub',
            position: 'right',
          },
        ],
      },
  ...
  ```


  </TabItem>
  <TabItem value="depois" label="Depois">
  ```js showLineNumbers title="docusaurus.config.js"
  ...
  themeConfig:
    /** @type {import('@docusaurus/preset-classic').ThemeConfig} */
    ({
      // Replace with your project's social card
      image: 'img/docusaurus-social-card.jpg',
      navbar: {
        title: 'My Site',
        logo: {
          alt: 'My Site Logo',
          src: 'img/logo.svg',
        },
        items: [
          {
            type: 'docSidebar',
            sidebarId: 'tutorialSidebar',
            position: 'left',
            label: 'Tutorial',
          },
          {
            href: 'https://github.com/facebook/docusaurus',
            label: 'GitHub',
            position: 'right',
          },
        ],
      },
  ...
  ```
  </TabItem>
</Tabs>

**Remover o atalho para o Blog no `footer`**

<Tabs>
  <TabItem value="antes" label="Antes" default>
  ```js showLineNumbers title="docusaurus.config.js"
  ...
    title: 'More',
    items: [
      // highlight-start
      {
        label: 'Blog',
        to: '/blog',
      },
      // highlight-end
      {
        label: 'GitHub',
        href: 'https://github.com/facebook/docusaurus',
      },
  ...
  ```

  </TabItem>
  <TabItem value="depois" label="Depois">
  ```js showLineNumbers title="docusaurus.config.js"
  ...
    title: 'More',
    items: [
      {
        label: 'GitHub',
        href: 'https://github.com/facebook/docusaurus',
      },
  ...
  ```
  </TabItem>
</Tabs>

Pronto! Já não temos mais a seção de blog.

### 2.2. Eliminando a página inicial

Para eliminar a página inicial, precisamos de três etapas:

1. Configurar a rota base do docs como `/`;
2. Adicionar um slug para `/` no front-matter de uma de nossas páginas de
   conteúdo; e
3. Eliminar o jsx e css relacionados à página inicial atual.

Para fazer a primeira etapa, basta editar novamente o arquivo
`docusaurus.config.js` como demonstrado a seguir:

<Tabs>
  <TabItem value="antes" label="Antes" default>
  ```js showLineNumbers title="docusaurus.config.js"
  ...
  presets: [
    [
      'classic',
      /** @type {import('@docusaurus/preset-classic').Options} */
      ({
        // highlight-start
        docs: {
          sidebarPath: './sidebars.js',
          // Please change this to your repo.
          // Remove this to remove the "edit this page" links.
          editUrl:
            'https://github.com/facebook/docusaurus/...',
        },
        // highlight-end
        blog: false,
        theme: {
          customCss: './src/css/custom.css',
        },
      }),
    ],
  ],
  ...
  ```
  </TabItem>
  <TabItem value="depois" label="Depois">
  ```js showLineNumbers title="docusaurus.config.js"
  ...
  presets: [
    [
      'classic',
      /** @type {import('@docusaurus/preset-classic').Options} */
      ({
        // highlight-start
        docs: {
          sidebarPath: './sidebars.js',
          // Please change this to your repo.
          // Remove this to remove the "edit this page" links.
          editUrl:
            'https://github.com/facebook/docusaurus/...',
          routeBasePath: '/'
        },
        // highlight-end
        blog: false,
        theme: {
          customCss: './src/css/custom.css',
        },
      }),
    ],
  ],
  ...
  ```
  </TabItem>
</Tabs>

A seguir, adicione o seguinte ao front matter do arquivo `md` ou `mdx` que você
quer que seja sua página inicial (não sabe o que é? Veja
[aqui](https://docusaurus.io/docs/create-doc#doc-front-matter)):

```md
---
title: <!--- Tanto faz -->
sidebar_position: <!--- Tanto faz -->
slug: /
---
```

Essa última alteração vai causar o seguinte warning:

```bash
[WARNING] Duplicate routes found!
- Attempting to create page at /, but a page already exists at this route.
This could lead to non-deterministic routing behavior.
```

Isso aparece pois a página inicial já existente também tenta receber a mesma
rota. Para eliminar esse problema, o mais fácil é deletá-la. Para isso, delete
o arquivo `src/index.js`. Pronto! Eliminamos a página inicial também!

## 3. Mudanças cosméticas

### 3.1. Editando o `custom.css`

O docusaurus nos permite editar um arquivo css que serve como referência global
para todas as páginas `jsx` ou `mdx` criadas em nossa documentação. Isso abre a
possibilidade para criar todo o tipo de customizações de
cores/animações/estilo. Vamos apenas modificar um pouco as cores. Para isso,
edite o arquivo `src/css/custom.css` para que fique assim:

```css showLineNumbers title="custom.css"
/**
 * Any CSS included here will be global. The classic template
 * bundles Infima by default. Infima is a CSS framework designed to
 * work well for content-centric websites.
 */

:root {
  --ifm-color-primary: #9e53bc;
  --ifm-color-primary-dark: #9446b3;
  --ifm-color-primary-darker: #8e43ac;
  --ifm-color-primary-darkest: #813d9c;
  --ifm-color-primary-light: #74378c;
  --ifm-color-primary-lighter: #6e3485;
  --ifm-color-primary-lightest: #5a2b6d;
  --ifm-code-font-size: 95%;
  --ifm-background-color: #fdfdfd;
  --docusaurus-highlighted-code-line-bg: rgba(0, 0, 0, 0.1);
}

/* For readability concerns, you should choose a lighter palette in dark mode. */
[data-theme='dark'] {
  --ifm-color-primary: #dc8add;
  --ifm-color-primary-dark: #d46ed5;
  --ifm-color-primary-darker: #d060d1;
  --ifm-color-primary-darkest: #cb52cd;
  --ifm-color-primary-light: #e4a6e5;
  --ifm-color-primary-lighter: #e8b4e9;
  --ifm-color-primary-lightest: #f5ddf5;
  --ifm-background-color: #000000;
  --docusaurus-highlighted-code-line-bg: rgba(0, 0, 0, 0.3);
}
```

### 3.2. Modificando o ícone do site

Agora vamos modificar o ícone e o favicon da nossa documentação. Para isso,
adicione um logo de sua escolha à sua pasta `static`. Essa pasta é especial no
sentido de que ela é colocada na base do diretório da sua página estática
quando esta é transformada em um artefato. 

A seguir, vamos editar novamente o arquivo `docusaurus.config.js` para que fique assim:

```js showLineNumbers title="docusaurus.config.js"
...
const config = {
  title: 'My Site',
  tagline: 'Dinosaurs are cool',
  // highlight-start
  favicon: 'img/inteli.svg',
  // highlight-end
...
  themeConfig:
    /** @type {import('@docusaurus/preset-classic').ThemeConfig} */
    ({
      // Replace with your project's social card
      image: 'img/docusaurus-social-card.jpg',
      navbar: {
        title: 'My Site',
        logo: {
          alt: 'My Site Logo',
          src: 'img/logo.svg',
        },
...
```

Pronto! Com essa introdução e dando uma lida geral na [documentação do
docusaurus](https://docusaurus.io/docs), você já deve agora saber mais do que o
suficiente para fazer uma documentação ~f#@!~ supimpa! =D

