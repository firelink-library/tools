---
title: Gerando uma API REST de um Arquivo
sidebar_position: 1
slug: /json-server
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Pessoal o objetivo desta seção é estudar a utilização da ferramenta: [Json-Server](https://github.com/typicode/json-server). Ela permite criar uma API Rest de um arquivo JSON que traz a estrutura de dados desejada.

Ela permite a exposição da API criada na rede local e também adição de novos dados.

## 1. Instalação

O ***Json-Server*** foi escrito em JavaScript, para sua utilização, vai ser necessária apenas o [Node.js](https://nodejs.org/pt)(recomendo a instalação utilizando o [nvm](https://github.com/nvm-sh/nvm)) instalado na máquina.

Para realizar a instalação do pacote, utilizar:

```bash
# Dentro do diretório do projeto
npm install json-server
```

## 2. Utilização

Agora para sua utilização, basta fornecermos um arquivo `json` que vai trazer a estrutura desejada. Por exemplo, este arquivo foi chamado de `meu-server.json`:

```json
{
    "usuarios":[
        { "id": 1, "name": "Murilo", "pass": "1234"},
        { "id": 2, "name": "Goku", "pass": "1234"},
        { "id": 3, "name": "Vegeta", "pass": "1234"}
    ],
    "posts":[
        {"id":1, "user_id":1, "post": "teste"},
        {"id":2, "user_id":1, "post": "teste234"},
        {"id":3, "user_id":2, "post": "mais uma lib JS?"},
        {"id":4, "user_id":3, "post": "pum"},
        {"id":5, "user_id":3, "post": "pum pum"}
    ]
}
```

Para executar o servidor, utilizar o comando:

```bash
npx json-server meu-server.json
```

Agora, no terminal que executamos o comando, vamos ver a seguitne mensagem:

```bash
JSON Server started on PORT :3000
Press CTRL-C to stop
Watching dados.json...

( ˶ˆ ᗜ ˆ˵ )

Index:
http://localhost:3000/

Static files:
Serving ./public directory if it exists

Endpoints:
http://localhost:3000/usuarios
http://localhost:3000/posts
```

Repare que além de trazer as rotas que estão disponíveis, ele também trouxe uma solução para fornecer arquivos estáticos.

## 3. Geração de Dados

Para facilitar o desenvolvimento, estou deixando mais um snippet de código para gerar esse arquivo json. Espero que ajude!

<Tabs
defaultValue="node"
values={[
{ label: 'Node.js 🐗', value: 'node' },
{ label: 'Python 🐍', value: 'python' },
{ label: 'Go 🐻', value: 'go' },
]}>

<TabItem value="node">
```js
/* Node.js (ESM ou CommonJS) */
const fs = require('fs');
const readline = require('readline');

const rl = readline.createInterface({ input: process.stdin, output: process.stdout });
const ask = q => new Promise(r => rl.question(q, r));

const NAMES = ['Murilo','Jessica','Andre','Lucas','Paula','Carlos','Fernanda','Beatriz','Rafaela','Daniel'];
const POSTS = ['teste','Mais uma lib JS?','Lorem ipsum','pum','pum pum','Hello world','Post aleatório'];

(async () => {
  const file = await ask('Nome do arquivo (sem extensão): ');
  const users = +await ask('Quantidade de usuários: ');
  const posts = +await ask('Quantidade de posts: ');

  const usuarios = Array.from({ length: users }, (_, i) => ({
    id: i + 1,
    name: NAMES[Math.floor(Math.random() * NAMES.length)] + (users > NAMES.length ? `_${i+1}` : ''),
    pass: Math.random().toString(36).slice(-8),
  }));

  const postsArr = Array.from({ length: posts }, (_, i) => ({
    id: i + 1,
    user_id: usuarios[Math.floor(Math.random() * usuarios.length)].id,
    post: POSTS[Math.floor(Math.random() * POSTS.length)],
  }));

  fs.writeFileSync(`${file}.json`, JSON.stringify({ usuarios, posts: postsArr }, null, 4));
  console.log(`✔ Criado ${file}.json`);
  rl.close();
})();
```
</TabItem> 
<TabItem value="python">
```py
#!/usr/bin/env python3
import json, random, secrets, pathlib

NAMES = ["Murilo","Jessica","Andre","Lucas","Paula",
         "Carlos","Fernanda","Beatriz","Rafaela","Daniel"]
POSTS = ["teste","Mais uma lib JS?","Lorem ipsum",
         "pum","pum pum","Hello world","Post aleatório"]

def rand_pass(n=8): return ''.join(secrets.choice("abcdefghijklmnopqrstuvwxyz0123456789") for _ in range(n))

def main():
    file = input("Nome do arquivo (sem extensão): ").strip()
    users = int(input("Quantidade de usuários: ") or 0)
    posts = int(input("Quantidade de posts: ") or 0)

    usuarios = [
        {"id": i+1,
         "name": random.choice(NAMES) + (f"_{i+1}" if users > len(NAMES) else ""),
         "pass": rand_pass()} for i in range(users)
    ]

    posts_arr = [
        {"id": i+1,
         "user_id": random.choice(usuarios)["id"],
         "post": random.choice(POSTS)} for i in range(posts)
    ]

    path = pathlib.Path(f"{file}.json")
    path.write_text(json.dumps({"usuarios": usuarios, "posts": posts_arr}, indent=4, ensure_ascii=False))
    print(f"✔ Criado {path.name}")

if __name__ == "__main__":
    main()
```
</TabItem> 
<TabItem value="go">
```go
package main

import (
	"bufio"
	"encoding/json"
	"fmt"
	"math/rand"
	"os"
	"strconv"
	"strings"
	"time"
)

var (
	names = []string{"Murilo","Jessica","Andre","Lucas","Paula",
		"Carlos","Fernanda","Beatriz","Rafaela","Daniel"}
	postsTxt = []string{"teste","Mais uma lib JS?","Lorem ipsum",
		"pum","pum pum","Hello world","Post aleatório"}
)

type Usuario struct{ ID int `json:"id"`; Name, Pass string `json:"name","pass"` }
type Post struct{ ID, UserID int `json:"id","user_id"`; Post string `json:"post"` }
type Data struct{ Usuarios []Usuario `json:"usuarios"`; Posts []Post `json:"posts"` }

func randPass(n int) string {
	const letters = "abcdefghijklmnopqrstuvwxyz0123456789"
	b := make([]byte, n)
	for i := range b { b[i] = letters[rand.Intn(len(letters))] }
	return string(b)
}

func ask(r *bufio.Reader, q string) string {
	fmt.Print(q)
	out, _ := r.ReadString('\n')
	return strings.TrimSpace(out)
}

func main() {
	rand.Seed(time.Now().UnixNano())
	in := bufio.NewReader(os.Stdin)

	file := ask(in, "Nome do arquivo (sem extensão): ")
	users, _ := strconv.Atoi(ask(in, "Quantidade de usuários: "))
	posts, _ := strconv.Atoi(ask(in, "Quantidade de posts: "))

	u := make([]Usuario, users)
	for i := 0; i < users; i++ {
		name := names[rand.Intn(len(names))]
		if users > len(names) { name = fmt.Sprintf("%s_%d", name, i+1) }
		u[i] = Usuario{i + 1, name, randPass(8)}
	}

	p := make([]Post, posts)
	for i := 0; i < posts; i++ {
		p[i] = Post{i + 1, u[rand.Intn(len(u))].ID, postsTxt[rand.Intn(len(postsTxt))]}
	}

	data, _ := json.MarshalIndent(Data{u, p}, "", "    ")
	os.WriteFile(file+".json", data, 0644)
	fmt.Printf("✔ Criado %s.json\n", file)
}
```
</TabItem> 
</Tabs>