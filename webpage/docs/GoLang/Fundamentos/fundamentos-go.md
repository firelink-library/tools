---
title: Fundamentos da Linguagem Go
sidebar_position: 1
slug: /fundamentos-go
---


## 1. Algumas definições importantes

- Pode ser utilizado para estudar com o playground: https://go.dev/play/
- Link para documentação: https://go.dev/doc/effective_go
- Go foi criado com os três pilares: *efficient compilation, efficient execution and ease of programming*.

---

## 2. Primeiro programa em Go

```go
// Line comments - Hello World from GoLang
package main

import "fmt"

func main() {
	fmt.Println("Hello, Mundo!")
}
/*Bloco de comentários!
Aqui várias linhas */
```

Quando compartilhando código para foruns, é interessante enviar o código da pergunta utilizando, por exemplo, o PlayGround. Ele permite que as pessoas editem e enviem sugestões de modificações para os autores.

Os programas para serem executados, eles devem possuir um pacote main. Dentro deste pacote `main`, é necessário uma função `main`, ela é o ponto de entrada do nosso projeto.

Todos os códigos de Go são organizados em pacotes. É a forma como nossos projetos ficam distribuídos e organizados. O pacote `fmt` é da biblioteca padrão do Go, ele permite utilizar as funções de entrada e saída, por exemplo.

```go
package main

import "fmt"

func main() {
	const nome = "Murilo Zanini"
	const idade = 36
	const peso = 108.5
	fmt.Println("Ola Mundo da Formatação!")
	fmt.Printf("Aqui vai uma string: %s\n", nome)
	fmt.Printf("Aqui vai um número inteiro: %d\n", idade)
	// Ultima linha de código da função não precisa do ;
	fmt.Printf("Aqui vai um número real: %.3f\n", peso)
}
```

Para ver mais detalhes de formatação: https://pkg.go.dev/fmt#Printf

A codificação UTF-8 é uma forma de armazenar os dados UNICODE dos caracteres de forma eficiente. Go utiliza UTF-8 e UNICODE para armazenar os dados. Para saber mais: 
- https://developer.mozilla.org/pt-BR/docs/Glossary/UTF-8
- https://www.ime.usp.br/~pf/algoritmos/apend/unicode.html
- https://www.w3schools.com/charsets/ref_html_utf8.asp

---

Go é uma linguagem estáticamente tipada. Isso significa que os tipos são definidos no momento da compilação do nosso programa e não em sua execução. As variáveis para serem utilizadas precisam ser declaradas. Nesse ponto, a atribuição pode ser realizada de algumas formas:

1. Atribuição com inicialização, não precisa definir o tipo da variável, ele é inferido de forma automática: `nome := "Murilo"`
2. ATENÇÃO: Variáveis e constantes são inicializadas de forma distinta em Go.
3. Para declarar uma variável e não atribuir um valor inicial para ela, é necessário utilizar o inicializador com valor zero: `var idade int`. Desta forma, a variável está inicializada com um valor inicial.
4. Quando um valor é atribuído a uma variável e ela não é utilizada, o código lança um erro quando ele tenta ser executado.

```go
package main

import "fmt"

func main() {
	// O ponto e virgula no final da expressa é opcional
	idade := 36
	fmt.Printf("Valor da idade: %d\n", idade)
	var nome string
	fmt.Printf("Nome informado: %s\n", nome)
	// ATENÇÃO: Strings utilizam ", chars únicos utilizam '
	nome = "Murilo"
	fmt.Printf("Nome depois da atribuição: %s\n", nome)
	// Multiplo inicializador e operador _
	a, b, _, d := 1, 2, 3, 4
	fmt.Printf("Valores informados: %d %d %d", a, b, d)
	// O operador _ é utilizado quando um valor de retorno é 
	// fornecido e ele não será utilizado no contexto.
}
```

O nulo do Golang é `nil`.

Para apresentação de valores em binário e hexadecimal:

```go
package main

import "fmt"

func main() {
	valor1, valor2 := 'a', 15
	fmt.Printf("Valor em binário: %b\n", valor1)
	fmt.Printf("Valor em hexadecimal: %x", valor2)

}
```

Para iniciar um valor além do zero inicial: `var a int = 42`. Para realizar o cast de tipo, utilizar: 

```go
package main

import "fmt"

func main() {
	var variavel1 int = 42
	variavel2 := float32(variavel1)
	fmt.Printf("Valor em inteiro: %d\n", variavel1)
	fmt.Printf("Valor em float: %f\n", variavel2)

	// Exibindo o tipo
	fmt.Printf("Tipo da variavel 1: %T\n", variavel1)
	fmt.Printf("Tipo da variavel 2: %T\n", variavel2)

}
```

Para utilizar mais de um pacote, utilizamos o `()` para descrever todos os pacotes que estamos importando.

```go
package main

// Doc da lib "math/rand" - https://pkg.go.dev/math/rand

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Printf("Valor aleatório 🎲: %d\n", rand.Intn(6))
}
```

IMPORTANTE: quando queremos que algo fique disponível fora do pacote que ele foi criado, utilizar letra maiúscula para descrever ela. Por exemplo, o valor `MeuValor`, fica disponível quando o pacote for importado, ela será exportada. Quando utilizamos o identificador `meuValor`, ele pode ser utilizado apenas dentro do pacote, ele não será exportado. Valor para funções. É equivalente ao conceito de público/privado de linguagens orientadas a objeto.

```go
package main

import (
	"fmt"
)

// Função não é exportada no pacote
func encontraMaior(x, y int) int {
	if x > y {
		return x
	}
	return y
}

// É possível retornar mais de um valor com uma função
func trocados(valor1 int, valor2 int, valor3 float32) (float32, int, int) {
	return valor3, valor2, valor1
}

func main() {
	x, y, z := trocados(10, 3, 4.)
	fmt.Printf("Chamda da função: %f\t%d\t%d\n", x, y, z)
}
```

Go suporte operações do tipo bitwise e bitshift. Para verificar mais sobre o que pode ser realizado com Go em nível de bit manipulation: https://pkg.go.dev/math/bits#pkg-overview.

Go possui um operador para trazer identificadores que são construídos com um incremento. Esse elemento é o `iota`. A documentação pode ser vista em: https://go.dev/wiki/Iota.

```go
package main

import (
	"fmt"
)

// Criando uma enumeração
type WeekDay int

const (
	domingo WeekDay = iota //Fica valendo 0
	segunda
	terca
	quarta
	quinta
	sexta
	sabado
)

func main() {
	fmt.Printf("Utilizando valores do enum: %d\t%d\n", domingo, sabado)
}
```

Para executar um programa em Go:

```bash
go run ./nome_arquivo.go
```

Para desenvolver os programas em Go utilizando o ambiente de desenvolvimento nativo, vamos precisar de algumas ferramentas:
- O compilador/runtime de Go
- Git instalado na máquina
- Um editor (no momento, o VS Code)
- Dependências de desenvolvimento (plugins do Go com VS Code)

Com a extensão de Go instalada no VS Code, utilizar o comando: `go install` para instalar as ferramentas e dependências de código. Selecionar todas e instalar. Todas as ferramentas são instaladas dentro do caminho indicado em $GOPATH.

Os módulos em GoLang são utilizados para realizar o `namespacing` das dependências do código. Desta forma é possível importar os módulos e realizar seu gerenciamento sem maiores problemas de conflito. Para iniciarmos um módulo, dentro do diretório da nossa solução, utilizar o comando: `go mod init nome/modulo`.

É possível compilar o programa para outras plataformas diferentes da de desenvolvimento utilizando Go. Verificar a documentação: https://go.dev/doc/tutorial/compile-install

O `mod` do Go é equivalente ao `pip` do Python. Para instalar as dependências listadas em um arquivo `mod` de um projeto, podemos utilizar o comando: `go mod tidy`. Mais sobre ele na documentação: https://go.dev/ref/mod .

Em GoLang, utilizamos o conceito de exportado ou não exportado para descrever o que está dentro do módulo/pacote ou apenas dentro dele.

Para importar um arquivo que está dentro do módulo, precisamos informar o caminho dele. Para isso, ele deve ter sua rota iniciada dentro do nome do pacote fornecido no comando de criar o pacote com o `go mod`.

Para um projeto com diversos diretórios, temos dentro do arquivo `puppy.go`:

```go 
package puppy

// Funções do pacote
func Bark() string{
	return "Au!"
}

func Barks() string{
	return "Ufufufufu!"
}
```

Agora dentro arquivo `main.go`:

```go
package main

import (
	"fmt"
	"modulos_projeto01/puppy"
)

func main() {
	fmt.Printf("%s\n", puppy.Bark())
	fmt.Printf("%s\n", puppy.Barks())
}
```

O que estiver no pacote `main` não precisa estar em um diretório separado para sua execução. Para fazer um pacote utilizar dependências dos demais, editar o arquivo `go.mod`, para que ele possa ver os pacotes:

```go
module modulos_projeto01

go 1.23.2
```

Dentro do `dog/funcoes.go`:

```go
package dog

import (
	"strings"
)

func BigDog(msg string) (string){
	return strings.ToUpper(msg)
}
```

Dentro do `puppy/puppy.go`:

```go
package puppy

import (
	"modulos_projeto01/dog"
)

// Funções do pacote
func Bark() string{
	return "Au!"
}

func Barks() string{
	return "Ufufufufu!"
}

func BigBark() string{
	return dog.BigDog(Bark())
}
```

E por fim, dentro da `main.go`:

```go
package main

import (
	"fmt"
	"modulos_projeto01/puppy"
)

func main() {
	fmt.Printf("%s\n", puppy.Bark())
	fmt.Printf("%s\n", puppy.Barks())
	fmt.Printf("%s\n", puppy.BigBark())
}
```

---

## 3. Estruturas de controle em Go

Retomando: os programas em Go são iniciados no pacote `main`, pela função `main`.

Estrutura de decisão `if` similar a do C, Java. O bloco de código do `if`, deve estar entre `{}`. A condição de verificação não precisa estar entre `()`. Podemos encadear as estruturas de decisão utilizando `else if`. Os operadores lógicos são os mesmos de C e Java.

A estrutura `switch` pode ser utilizada de algumas maneiras distintas:

```go
package main

import "fmt"

func main() {
	x := 10

	// Exemplo de utilização de switch
	// Caso 1
	switch {
	case x > 5:
		{
			fmt.Printf("Valor maior que 5\n")
		}
	case x < 5:
		{
			fmt.Printf("Aqui vai mais um!\n")
		}
	default:
		{
			fmt.Printf("Valor padrão\n")
		}
	}

	// Caso 2
	switch x {
	case 1:
		{
			fmt.Printf("O que fazer com o valor 1\n")
		}
	case 2:
		{
			fmt.Printf("Aqui para o 2\n")
		}
	}
}

```

Existe um operador chamado de `select`, ele funciona de forma similar ao `switch`, mas para o contexto de paralelismo e comunicação entre canais. Mais sobre o tema logo menos.

O loop `for` pode ser utilizado de algumas formas distintas:

```go
package main

import "fmt"

func main(){
	// Primeiro exemplo de utilização de for
	for x:= 0; x < 10; x++{
		fmt.Printf("Primeiro Exemplo do For - %d\n", x)
	}

	// Segundo exemplo de utilização de for
	x := 0
	for x < 10 {
		fmt.Printf("Segundo Exemplo do For - %d\n", x)
		x++
	}

	// Terceiro exemplo de utilização do for
	x = 0
	for{
		fmt.Printf("Terceiro Exemplo do For - %d\n", x)
		x++
		if x == 10 {
			break
		}
	}
}
```

É possível realizar interações uma dentro da outra (loops internos). Existe uma outra variação do for que permite utilizar ele para varrer um conjunto de valores dentro de um slice (similar a uma lista). Também pode ser utilizado com um mapa.

```go
package main

import "fmt"

func main(){
	// Criando um slice
	x := [] int{42, 34, 56, 78, 90, 12}

	// Utilizando um for para interar por todos os valores
	for i, valor := range x{
		fmt.Printf("Valor na posição %d \t %d\n", i, valor)
	}

	// Utilizando a mesma lógica para navegar em mapas
	y := map[string]int{
		"Murilo":36,
		"Goku":42, "Vegeta":44,
	}

	for chave, valor := range y{
		fmt.Printf("Valor declarado como chave: %s\t e o conteúdo: %d\n", chave, valor)
	}
}
```

---

Em muitas situações, é conveniente utilizar alguns tipos de dados que permitem trabalhar com diversos valores agregados. A linguagem Go traz alguns tipos agregados que permitem realizar esse tipo de manipulação. Essas estruturas são chamadas de `aggregate data types`.


Os tipos de dados agregados em Go são:

- `array`: sequencia do mesmo tipo de dados. Não muda de tamanho. Em geral, utilizado nas implementações internas de Go.
- `slice`: construído sobre as características de um array, portanto só podem armazenar valores do mesmo tipo. Podem mudar seu tamanho. Possuem um comprimento e uma capacidade.
- `map`: armazenam um conjunto de chaves e valores, cada um de um tipo respectivo. Os valores não são armazenados de forma sequencia ou ordenada.
- `struct`: tipo composto de dados que permite representar um conjunto de diferentes variáveis.

## 4. Arrays

Exemplo de utilização de arrays:

```go
package main

import "fmt"

func main(){
	// Declara um array e realiza algumas manipulações com ele
	// Determinamos o nome do array, seu tamanho e seu tipo
	var meuArray [10]int

	// Imprime o array
	fmt.Printf("%#v\t Tipo do arrat: %T\n", meuArray, meuArray)

	// Para imprimir o array de forma não estruturada
	fmt.Printf("%v\n", meuArray)

	// Atribuindo um valor para o array
	meuArray[0] = 10
	meuArray[1] = meuArray[0]/3

	// Imprimi o array novamente
	fmt.Printf("%v\n", meuArray)

	// Declara e inicializa o array
	// Posições não iniciadas, tem seu valores zerado/nulo atribuído a elas.
	nomes := [5]string{"Murilo", "Goku", "Vegeta",}

	// Declara o array e deixa o Go inferir a quantidade de memória necessária
	idades := [...]int{36,29,9}

	// Imprime o array
	fmt.Printf("%#v\t Tipo do array: %T\n", nomes, nomes)
	fmt.Printf("%#v\t Tipo do array: %T\n", idades, idades)

	// Utiliza o tamanho do array
	fmt.Printf("Tamanho do array: %d\n", len(idades))
}
```

## 5. Slices

Slices são como arrays, mas eles podem ter seu tamanho alterado dinamicamente. Portanto mais elemento podem ser adicionados a ele. Os slices podem ser utilizados em conjunto com a função range também. Alguns detalhes de implementação dos slices:

```go
package main

import (
	"fmt"
	"strconv" //Para os casts de tipo
)

// GOlang não suporta overloading de funções
func MostrarSliceString(lista []string){
	fmt.Printf("Conteúdo atual do Slice: %v\n", lista)
}


func MostrarSliceInt(lista []int){
	fmt.Printf("Conteúdo atual do Slice: %v\n", lista)
}


func main(){

	// Criando um slice
	// Aqui o slice é instânciado mas não tem nenhum valor atribuído a ele
	meu_slice := []string{}	

	MostrarSliceString(meu_slice)

	// Adicionando elementos ao slice
	// Importante notar aqui: O append adiciona um novo elemento no slice, mas ele precisa realizar a reatribuição, que o retorno da função, caso contrário, ele não modifica o slice enviado para ele.
	_ = append(meu_slice, "entra aqui!")

	MostrarSliceString(meu_slice)

	// Com a reatribuição
	meu_slice = append(meu_slice, "Agora sim entra aqui")

	MostrarSliceString(meu_slice)

	// Instanciando e inicializando um slice
	novo_slice := []int{4, 5, 9, -78}

	// Converter um inteiro para string e appenda no slice
	meu_slice = append(meu_slice, strconv.Itoa(novo_slice[0]))

	MostrarSliceInt(novo_slice)
	MostrarSliceString(meu_slice)


	// Utilizando o for-range
	for indice, valor := range novo_slice{
		fmt.Printf("%d valor na posição %d\n", indice, valor)
	}
}
```


Ao tentar acessar um posição que não está dentro do range de um slice, um erro vai ser lançado. Partes de um slice podem ser acessadas utilizando os indices, como as listas em Python.

```go
package main

import "fmt"

func imprimir(v []int) {
	fmt.Printf("%v\n", v)
}

func algumaCoisa() {
	meu_slice := []int{4, 5, 8, 9}
	parte_1 := meu_slice[0:2] //4,5
	parte_2 := meu_slice[:3]  //4,5,8
	parte_3 := meu_slice[2:]  //8,9
	imprimir(meu_slice)
	imprimir(parte_1)
	imprimir(parte_2)
	imprimir(parte_3)
}

func main() {
	fmt.Println("Hello, 世界")
	algumaCoisa()
}
```


Importante, para remover um elemento do slice, fazemos uma cópia sem ele.

```go
func RemoveIndex(s []int, index int) []int {
    return append(s[:index], s[index+1:]...)
}
```

Utilizando a função `make()`, é possível reservar memória para utilizar os elementos de um slice que serão conhecidos (espaço de memória que será utilizado). Esse espaço fica reservado, mas não altera o tamanho atual do slice.

```go
// Pacote e código anterios

func verificandoSlice(lista []string){
	fmt.Printf("Elemento recebido: %v\t Size: %d Capacidade: %d\n", lista, len(lista), cap(lista))
}

func utilizandoMake(){
	// Utilizando o make para alocar memória para um slice
	// O slice é iniciado com 0 elementos e reservando 10 posições de memória
	nomes := make([]string, 0, 10)	
	verificandoSlice(nomes)
	nomes = append(nomes, "Murilo")
	nomes = append(nomes, "Vegeta")
	verificandoSlice(nomes)
	nomes = append(nomes, "Goku")
	verificandoSlice(nomes)
}

func main(){
	utilizandoMake()	
}
```

É possível utilizar um slice de slices em Go. É como utilizar uma matriz de elementos.

```go
func trabalhandoComSliceDeSlice(){
	gigante := [][]int{}
	gigante = append(gigante, []int{1,2,3})
	// Podem ser de tamanhos distintos
	gigante = append(gigante, []int{4,5,})
	fmt.Println(gigante)
	fmt.Println("Exibindo apenas uma posição:", gigante[0][1])
	fmt.Println("Exibindo número de linhas (quantos slices dentro):", len(gigante))
}

func main(){
	trabalhandoComSliceDeSlice()	
}
```

Arrays, slices e outras estruturas em Go são enviados por valor. Para passar eles por referência, é necessário enviar eles utilizando um ponteiro.

## 6. Maps

Os mapas são uma forma de construir estruturas do tipo chave-valor, com os mesmos tipos de dados em cada elemento da estrutura. Sua sintaxe é `variavel := map[tipo_chave] tipo_valor{ chave:valor, chave2:valor2}`. Alguns exemplos de manipulação de dicionários.

```go
package main

import (
	"fmt"
)

func Funcionalidade_01(){
	// Cria o literal de um mapa
	idades := map[string]int{
		"Murilo":36,
		"Vegeta":44,
		"Goku":42,
	}

	// Exibe todo o mapa
	fmt.Println(idades)

	// Altera o valor da idade de uma chave
	idades["Goku"] = 10
	fmt.Println(idades)

	// Inserindo valores nos mapas
	idades["Bulma"] = 35
	fmt.Println(idades)

	// Acessando todos os elementos dentro do mapa
	for chave, valor := range(idades){
		string_saida := fmt.Sprintf("Valor %d com chave %s", valor, chave)
		fmt.Println(string_saida)
	}

	// Testando se existe uma chave. Se o valor não for utilizado, um _ pode ser utilizado.
	valor, ok := idades["Blonko"]	//Verifica se a chave existe
	if ok{
		fmt.Println("Valor da chave:", valor)
	} else {
		fmt.Println("Essa chave não existe")
	}

	// Para deletar uma chave
	// No caso de uma deleção de chave que não existe, nada é alterado no mapa.
	delete(idades, "Teste")

}

func main(){
	Funcionalidade_01()
}
```

Verificar essa implementação:

```go
package main

import (
	"fmt"
)

func Funcionalidade_02(){
	// Criando um mapa para listas
	comidas := map[string] []string{
		"Murilo" : {"Lamen", "Macarrão", "Pizza",},
		"Vegeta" : {"Hambuguer", "Doces"},
		"Goku" : {"Lamen", "Hambuguer", "Hotdog",},
	}

	// Passando pelos elementos do mapa
	for chave, _ := range(comidas){
		fmt.Printf("%s gosta de: ", chave)
		for _, dado := range(comidas[chave]) {
			fmt.Printf("%s\t", dado)
		}
		fmt.Println()
	}
}

func main(){
	Funcionalidade_02()
}
```


## 7. Structs

Utilizando estruturas do tipo `Struct`, podemos colocar valores de tipos distintos no mesmo tipo abstrato de dado. As estruturas são muito semelhantes aos structs da linguagem C. Os elementos da struct podem ser acessados como os itens das estruturas em C, utilizando o operador ponto.

```go
package main

import "fmt"

// Declaração das estruturas que são utilizadas no programa
type person struct{
	primeiroNome string
	sobreNome string
	idade int
}

// A estrutura pode ser instânciada como uma variável

func TesteFuncionalidade01(){
	p1 := person{
		primeiroNome: "Murilo",
		sobreNome: "Carvalho",
		idade: 36,
	}

	p2 := person{"Kakaroto", "Goku", 42}

	p3 := person{
		idade: 44,
		primeiroNome: "Vegeta",
		sobreNome: "Prince",
	}

	// Exibe as três pessoas
	fmt.Println(p1)
	fmt.Println(p2)
	fmt.Println(p3)

	// Acessa um elemento da struct
	fmt.Println("Nome de p1:", p1.primeiroNome)
}

func main(){
	TesteFuncionalidade01()
}
```


Structs podem ser utilizados dentro de outros structs (struct embedding). Neste caso, colocar os construtores (inicializadores) dentro da construção da estrutura mais externa (quando for necessário).

```go
package main

import "fmt"

// Declaração das estruturas que são utilizadas no programa
type person struct{
	primeiroNome string
	sobreNome string
	idade int
}


// Criando mais uma estrutura
type professor struct{
	pessoa person
	especialidade string
}

func TesteFuncionalidade02(){
	// Criando uma estrutura que possui outra estrutura dentro dela
	p1 := professor{
		pessoa: person{
			primeiroNome: "Murilo",
			sobreNome: "Carvalho",
			// Valores não inicializados, tem o valor 0 ou nil atribuídos a eles.
		},
		especialidade: "Computação",
	}

	fmt.Println(p1)
}

func main(){
	TesteFuncionalidade02()
}
```

É possível ter estruturas anônimas. Elas são definidas quando apenas os tipos da struct são definidos e os valores já são inicializados. Go também permite utilizar composição. Com as composições, os elementos internos podem ser acessados pelos elementos externos. Portanto, funções associadas aos tipos internos, estarão acessíveis para os elementos mais externos quando estes possuírem instâncias internas suas. Este comportamento da ao Go um mecanismo similar ao de herança e um mecanismo polimórfico a linguagem.

---

## 8. Funções

Funções são uma forma de agrupar código. Isso terna o código desenvolvido mais simples de se reutilizar, compreender e manutenível. Este comportamento também traz maior capacidade de abstração para nosso código.

As funções possuem a seguinte estrutura básica: `func (receiver) nomeDaFuncao (parametrosESeusTipos) tipoDeRetornoDaFuncao {codigoDaFuncao}`. Um detalhe importante: definimos as funções descrevendo seus parâmetros. Utilizamos uma função informando seus argumentos.

IMPORTANTE: Tudo em Go é passado por ***VALOR***. Uma função pode ter nenhum, um ou quantos tipo de retorno for necessário.

Uma função com o número de parâmetros variados é possível utilizando a notação de um parâmetro variático. Eles são enviados como um slice para a função. IMPORTANTE: um parâmetro variável deve ser o último declaro na função.

```go
package main

import "fmt"

// Função com parâmetros variáveis, pode ser qualquer quantidade
func adicionaValores(valores ...int) (int, int){
	total := 0
	for _, valor := range(valores){
		total += valor
	}
	return total, len(valores)
}

func main(){
	// Chamando função adicionaValores
	fmt.Println(adicionaValores(1,2,3,4))
	fmt.Println(adicionaValores(1,2,3,4,5,6,7,8,9))
	// Enviando diversos valores, extraíndo todos eles
	valores := []int{3,4,5,6,7}
	fmt.Println(adicionaValores(valores...))
}
```

A extração de todos os elementos de um array/slice, é chamado de Unfurling. Todos os valores são extraído e enviados para uma função, por exemplo. IMPORTANTE: sem este operador, estamos enviando apenas um parâmetro. Com ele, estamos enviando a quantidade de elementos que o slice possuir de parâmetros.

O operador `defer` faz com que a chamada de uma função não seja resolvida no momento de sua realização. Desta forma, o sistema empilha sua chamada, resolve a função atual e quando ela termina, executa a função com `defer`.

```go
package main

import "fmt"

func comportamento_02(){
	defer ola1()
	ola2()
}

// Para compreender a utilização do defer
func ola1(){
	fmt.Println("Ola 1")
} 

func ola2(){
	fmt.Println("Ola 2")
} 

func main(){
	comportamento_02()
}
```

Em geral, quando fazemos a alocação de algum recurso, como abrir uma conexão, um arquivo, utilizamos o `defer` para liberar este recurso.

É possível criar métodos em Go. Desta forma, as structs podem ter comportamentos associados a elas.

```go
package main

import "fmt"

// Criando métodos em Go
type Pessoa struct{
	nome string
	idade int
}

func (p Pessoa) DescrevePessoa(){
	fmt.Printf("Nome: %s\t Idade: %d\n", p.nome, p.idade)
}

func comportamento_03(){
	p1 := Pessoa{"Murilo", 36}
	p2 := Pessoa{"Jéssica", 29}
	p1.DescrevePessoa()
	p2.DescrevePessoa()
}

func main(){
	comportamento_03()
}
```

Em Go, interfaces declaram um conjunto de assinaturas para métodos. Desta forma, quem implementa aquelas interfaces, devem possuir uma implementação destes métodos. A capacidade polimórfica é a habilidade de um tipo realizar um comportamento de um outro tipo.

Em Go, os valores podem possuir mais de um tipo. Isso permite que realizamos a implementação do polimorfismo. Uma interface em Go é implementada utilozando a palavra `interface`, na frente do seu nome. Desta forma, implementamos a sobrecarga de funções utilizando o polimorfismo. Qualquer estrutura que implementar os métodos da interface, também vai ser do tipo da interface. CUIDADO: Observar o código a seguir com bastante cuidado para compreender o conceito apresentado.

```go
package main

import "fmt"

// Criando métodos em Go
type Pessoa struct{
	nome string
	idade int
}

func (p Pessoa) DescrevePessoa(){
	fmt.Printf("Nome: %s\t Idade: %d\n", p.nome, p.idade)
}

type PessoaEspecial struct{
	pessoa Pessoa
	altura float32
}

// Método da estrutura PessoaEspecial
func (p PessoaEspecial) DescrevePessoa(){
	fmt.Printf("Altura: %.2f\t", p.altura)
	p.pessoa.DescrevePessoa()
}

// Interface que traz uma assinatura. Todos que implementarem todos os seus métodos são deste tipo também
type Human interface{
	DescrevePessoa()
}

// Função para implementar o polimorfismo
func Descrever(h Human){
	h.DescrevePessoa()
}

func comportamento_04(){
	p1 := Pessoa{"Murilo", 36}
	p2 := PessoaEspecial{Pessoa{"Jéssica", 29}, 1.49}
	Descrever(p1)
	Descrever(p2)
}

func main(){
	comportamento_04()
}
```


Existe uma interface chamada `Stringer`, que permite realizar o log de estruturas e elementos no código. Estruturas que possuem o método `String() string` implementa essa interface. Não precisa ser apenas uma estrutura, pode estar associado a uma variável, por exemplo.

```go
package main

import (
	"fmt"
	"strconv"
)

// Estudo da implementação da interface Stringer()

type Usuario struct{
	nick string
	pass string
	nivel int
}

// Cria uma implementação sobre um valor
type Teste int

func (u Usuario) String() string{
	return fmt.Sprintf("Usuario{nick:%s,pass:%s,elo:%d}", u.nick,u.pass,u.nivel)
}

func (t Teste) String() string{
	return fmt.Sprintf("Valor do Teste: %s", strconv.Itoa(int(t)))
}

func main(){
	user := Usuario{"Murilo","123456",5}
	fmt.Println(user)
	teste := Teste(10)
	fmt.Println(teste)
}
```


Em Go, existe um pacote padrão para lidar com logs da execução do programa. Ele é importado do pacote `"log"`. Ele possui as funções impressão na saída padrão como o "fmt". 

Lembrando, podemos implementar uma enumeração no Go utilizando `iota`. Ela é implementada como uma sequencia de inteiros. Go permite utilizar Wrapper Functions, que são funções que encapsulam comportamentos. Desta forma, é possível direcionar um comportamento utilizando elas.

ATENÇÃO: Estudar o código a seguir com cuidado, tem vários detalhes importantes nele.

```go
package main

import (
	"fmt"
	"log"
)

// Define algumas estruturas para utilizar 
type User struct{
	name string
	acessLevel AcessLevels
}

// Cria uma enumeração quanto ao nível de acesso
type AcessLevels int
const (
	Visitante AcessLevels = iota
	Funcionario
	Administrador
	Dono
)
// Implementa a interface Stringer para utilizar a string
func (al AcessLevels) String() string{
	// Utiliza o operador spread para encontrar o equivalente ao nível
	return [...]string{"Visitante", "Funcionario", "Administrador","Dono"}[al]
}

func (user User) String() string{
	return fmt.Sprintf("User{name:%s, acess: %s}", user.name, user.acessLevel)
}

// Wrapper Function para o comportamento de Log
// Está função recebe elementos que implementam a interface
// Ela vai interceptar a chamada da função log
func logInfo(s fmt.Stringer){
	log.Println("LOG REALIZADO NA APLICAÇÃO: ", s)
}

func main(){
	u1 := User{"Murilo", Dono}
	u2 := User{"Vegeta", Administrador}
	u3 := User{"Goku", Funcionario}

	log.Println(u1)

	users := []User{u1,u2,u3}
	for _, user := range(users){
		logInfo(user)
	}
}
```

## 9. Log e Escrita de Arquivos (Writter)

Primeiro vamos verificar como escrever um arquivo. Ele já está com algumas implementações futuras, mas ele é iniciado desta forma:

```go
package main

// Pacote para realizar a interface de writer
import (
	"io"
	"log"
	"os"
)

type Person struct{
	name string
}

// Interface de Writer, que recebe algo para ser escrito e retorna um erro se for preciso.
func (p Person) writeOut (w io.Writer) error{
	_, err := w.Write([]byte(p.name))
	return err
}

// Função para verificar se um erro aconteceu
func temError(e error) bool{
	if e == nil{
		return false
	}
	log.Fatalf("Erro: %s", e)
	// Nunca chega aqui
	return true
}
func main(){
	// Cria um arquivo
	arquivo, err := os.Create("teste.txt")

	// Testa para verificar se ocorreu um erro na criação do arquivo
	temError(err)

	// Adicionar o encerramento do arquivo
	defer arquivo.Close()

	// Cria um slice para enviar para o arquivo
	s := []byte("Ola Mundo!!")

	// Escreve os bytes no arquivo
	// Atenção ao detalhes, nesse caso, a variável `err` já existe
	_, err = arquivo.Write(s)

	temError(err)

}
```

Uma string é um pouco diferente de um slice de bytes. É possível converter de um tipo para o outro. Em geral, os printer possuem um buffer. Isso é implementado para que um conjunto temporário possa acomodar um conjunto de valores antes de sua utilização.


```go
package main

// Pacote para realizar a interface de writer
import (
	"bytes"
	"io"
	"log"
	"os"
	"fmt"
)

type Person struct{
	name string
}

// Interface de Writer, que recebe algo para ser escrito e retorna um erro se for preciso.
func (p Person) writeOut (w io.Writer) error{
	_, err := w.Write([]byte(p.name))
	return err
}

// Função para verificar se um erro aconteceu
func temError(e error) bool{
	if e == nil{
		return false
	}
	log.Fatalf("Erro: %s", e)
	// Nunca chega aqui
	return true
}
func main(){
	// Cria um arquivo
	arquivo, err := os.Create("teste.txt")

	// Testa para verificar se ocorreu um erro na criação do arquivo
	temError(err)

	// Adicionar o encerramento do arquivo
	defer arquivo.Close()

	// Cria um buffer de bytes
	var buffer bytes.Buffer

	// Cria uma pessoa
	p := Person{"Murilo"}

	// Escreve o conteúdo de pessoa no buffer e no arquivo
	// Arquivo
	p.writeOut(arquivo)
	// No endereço do buffer - trabalha com ponteiros a função writeOut
	p.writeOut(&buffer)

	// Escreve o conteúdo do buffer na tela
	fmt.Println(buffer.String())
}
```

Está é uma demonstração do uso de interfaces do Go.

---

## 10. Funções Anônimas

É um função que não possui um nome para invocação, apenas um comportamento e sua chamada.

```go
package main

import "fmt"

// Função tradicional
func mostrar(s string){
	fmt.Println(s)
}

func main(){
	// Chamando função tradicional
	mostrar("Murilo")

	// Declarando e executando uma função anônima
	func(s string){
		fmt.Println(s)
	}("Murilo")
}
```

Funções são cidadãos de primeira classe em Go, o que significa que eles podem ser considerados como um tipo. Portanto, podem ser atribuídos para variáveis. Elas também podem ser enviadas como parâmetros em outras funções.

```go
package main

import "fmt"

// Função tradicional
func mostrar(s string){
	fmt.Println(s)
}

func main(){
	// Chamando função tradicional
	mostrar("Murilo")

	// Declarando e executando uma função anônima
	func(s string){
		fmt.Println(s)
	}("Murilo")

	// Atribuíndo uma função a uma variável
	x := mostrar

	// Chamando a função pela variável
	x("Teste")

	// Atribuindo uma função anônima
	y := func(x,y int) int {
		return x+y
	}

	fmt.Println(y(3,4))
}
```

Quando retornar uma função, devolver apenas o nome da função, assim seu endereço será atribuído ao valor que invocou a função que a devolveu.


Em geral, funções enviadas como argumentos, estão enviando um `callback` para essa função. Em geral, permite que a função que recebeu esse argumento a execute quando for preciso.

Quando enviando uma função como callback, enviamos a assinatura da função no parâmetro.

```go
package main

import "fmt"

// Definindo uma fun;cão
func operacao(a int, b int, c func(int, int) int) int{
	return c(a,b)
}


func somar(a int, b int) int {
	return a+b
}

func subtrair(a int, b int) int {
	return a-b
}

func multiplicar(a int, b int) int {
	return a*b
}

func dividir(a int, b int) int {
	return a/b
}

func main(){
	// Cria uma slice com as funções
// Atenção: o tipo func() deve coincidir com as assinaturas das funçoes utilizadas.
	funcoes := []func(int,int)int {somar, subtrair, dividir, multiplicar,}

	a := 10
	b := 5

	// Chamndo as diversas operações
	for _, funcao := range(funcoes){
		fmt.Println(operacao(a,b,funcao))
	}
}
```

Closures são funções dentro de funções. Elas são chamadas a cada chamada e execução da função mais externa. Ele mantém, no caso do exemplo abaixo, o valor da variável interna do Closure.

```go
package main

import "fmt"

func TesteClosure() func() int{
	x := 0
	return func ()int{ 
		x++
		return x
	}
}

func main(){
	// Atribuí o closure para uma variável
	teste_closure := TesteClosure()

	fmt.Println(teste_closure())
	fmt.Println(teste_closure())
	fmt.Println(teste_closure())
}

// Saída: 1, 2, 3
```

### IMPORTANTE: Wrapper Functions

Retomando: Wrapper Functions permitem trazer mais uma camada de abstração para outra função. Ela traz outras funcionalidades para uma função que já está implementada.

***Importante:*** Quando utilizamos `defer` nas funções, elas são empilhadas em uma estrutura LIFO, portanto, a última função deferida, será a primeira resolvida.



---


## 11. Implementações de Testes com Go

Os arquivos de teste em Go precisam seguir algumas convenções de nome para ser utilizados. Os arquivos de teste ficam no mesmo pacote, mas importam o módulo `"testing"`. Quando vamos testar uma função, devemos criar o teste dela com outra função com o nome `TestNomeFuncao(t * testing.T)`.

Arquivo `main.go`:

```go
package main

func Somar(valores ...int) int {
	total := 0
	for _,valor := range(valores){
		total += valor
	}
	return total
}

func main(){

}
```

Arquivo `main_test.go`:

```go
package main

import "testing"

func TestSomar(t *testing.T){
	// Primeiro Teste
	valores := []int{4,6,7,8}
	total := Somar(valores...)
	if total != 25 {
		t.Errorf("Somatoria incorreta, esperado %d, recebido %d", 25, total)
	}

	// Segundo Teste
	total = Somar(3,4,5)
	if total != 12{
		t.Errorf("Somatoria incorreta, esperado %d, recebido %d", 12, total)
	}
}
```

Para executar o teste, rodar o comando: `go test`.
Observações importantes antes de seguir:
- O projeto deve estar em um módulo para rodar os testes. É importante que esse módulo não tenho o nome de `main`, caso contrário não será possível importar o arquivo main.go para rodar os testes.
- Para iniciar o módulo: `go mod init nomeDoModulo`
- Para rodar os testes: `go test`, no diretório com os arquivos de teste, senão dar o endereço do diretório.

Para documentar um programa, devemos apenas colocar os comentários antes da função que vamos documentar. Iniciamos nossa documentação com o nome da Função/elemento que vamos documentar. A documentação completa pode ser gerada utilizando a ferramenta `go doc`.

## ATENÇÃO: Precisa ser ajustado, não está implementado corretamente.


---

## 12. Ponteiros

Ponteiros permitem trabalhar com posições de memória em GoLang. O operador `&` nos da o endereço de uma variável. Os ponteiros em Go são muito semelhantes aos ponteiros em C. Lembrar que um ponteiro é um endereço de memória também.

```go
package main

import "fmt"


// Estudo do uso de ponteiros
func main(){
	x:=42
	fmt.Println(x)
	fmt.Println(&x)
	fmt.Printf("%v\t%T", &x,&x)
}
```

A saída para execução deste código:
```sh
42
0xc00000a0d8
0xc00000a0d8    *int
```

Um \* na frente de um tipo indica que é um ponteiro. No caso da saída produzida acima, estamos falando de um ponteiro para um número inteiro. O operador \* é utilizado para derreferenciar uma posição de memória. Ele acessa o que está dentro do conteúdo da variável. 

```go
package main

import "fmt"


// Estudo do uso de ponteiros
func main(){
	x:=42
	// Cria um ponteiro para x
	y := &x

	// Mostra o valor de x
	fmt.Println(x)
	// Mostra o endereço de x, que é o valor armazenado em y
	fmt.Println(y)
	// Mostra o valor de x, por derreferenciar y
	fmt.Println(*y)
	// Mostra o endereço de x
	fmt.Println(&x)
	// Mostra o endereço de y
	fmt.Println(&y)
}
```

A saída do programa:

```sh
42
0xc00000a0d8
42
0xc00000a0d8
0xc00004c050
```

Podemos enviar endereços para funções, assim qualquer mudança realizada nela vai alterar os valores do ponto que fez a chamada.

```go
package main

import "fmt"

// Função que recebe por valor
func Dobro(x int){
	x = 2*x
}

// Função que recebe por referncia
func DobroRef(x *int){
	*x = 2 * (*x)
}
// Estudo do uso de ponteiros
func main(){
	x:=42
	
	// Chama por valor
	Dobro(x)
	fmt.Println(x)
	// Chama por referencia
	DobroRef(&x)
	fmt.Println(x)
}
```

IMPORTANTE: Sempre que possível, trabalhar com passagem por valor, isso simplifica a utilização e depuração do funcionamento do programa. Pois torna mais claro os pontos que estão modificando o funcionamento do programa.

- ***Value Semantics:*** Passagem por valor. É o modo padrão de trabalho do GoLang.
- ***Pointer Semantics:*** Passagem de valor por referência. A função pode modificar o elemento dentro da função. Quando utilizamos grande quantidade de dados armazenados, pode ser uma abordagem interessante.

A função `init()` é executada antes da função `main()`. Em geral é utilizada para inicializar algum parâmetro ou elemento do nosso programa.

---

## 13. Tipos Genéricos

São tipos de dados que podem assumir um conjunto de valores diferentes. Desta forma, quando diferentes tipos puderem ser aceitos em uma função, podemos utilizar este comportamento.

```go
package main

import "fmt"

// Utilizando funções que não genéricas
func SomaI(a,b int) int{
	return a+b
}

func SomaF(a,b float64) float64{
	return a+b
}

// Utilizando tipos genéricos
func Soma [T int | float64](a,b T) T{
	return a+b
}

func main(){
	i1 := 10
	i2 := 20
	f1:=32.0
	f2 := 10.0
	fmt.Println("Soma Inteiros:", SomaI(i1,i2))
	fmt.Println("Soma Reais:", SomaF(f1,f2))
	fmt.Println("Soma Inteiros:", Soma(i1,i2))
	fmt.Println("Soma Reais:", Soma(f1,f2))
}
```

Este mesmo comportamento pode ser implementado utilizando interfaces.

```go
package main

import "fmt"

// Utilizando funções que não genéricas
func SomaI(a,b int) int{
	return a+b
}

func SomaF(a,b float64) float64{
	return a+b
}

// Utilizando tipos genéricos
type MeusNumeros interface{
	int | float64
}

func Soma [T MeusNumeros](a,b T) T{
	return a+b
}

func main(){
	i1 := 10
	i2 := 20
	f1:=32.0
	f2 := 10.0
	fmt.Println("Soma Inteiros:", SomaI(i1,i2))
	fmt.Println("Soma Reais:", SomaF(f1,f2))
	fmt.Println("Soma Inteiros:", Soma(i1,i2))
	fmt.Println("Soma Reais:", Soma(f1,f2))
}
```

Quando utilizamos o operador `~` na frente de um tipo, estamos indicando que qualquer alias para aquele tipo serão consideradas como o tipo básico na utilização do tipo genérico.

---

## 14. Aplicações

O gerenciamento de erros em Go é realizado, em geral, logo depois que um erro pode acontecer. Em Go não procuramos exceções, mas sim, verificamos se algum erro ocorreu no momento que ele poderia acontecer (retorno de uma função por exemplo).

IMPORTANTE: Uma string é um conjunto de bytes. Essa definição é muito importante, pois diversas funções utilizam um slice de bytes `[]bytes` para funcionar.

Existe, em GoLang, duas formas de codificar algo em JSON, referentes a forma como é realizado o processo de mapear os tipos de dados de JSON para os primitivos de Go:
- ***Marshaling:*** Processo de transformar uma estrutura do Go (ou mapa com chaves como Strings) para JSON. IMPORTANTE: Os campos devem ser exportados (iniciar com letra maiuscula)
- ***Unmarshaling:*** Processo de trazer dados em JSON (slice de `[]bytes`) para uma estrutura Go.

Para maiores informações, consultar a documentação aqui: https://go.dev/blog/json

```go
package main

import (
	"encoding/json"
	"fmt"
	"log"
)

// Criando as estruturas que serão utilizadas

type Person struct{
	First string
	Last string
	Age int
}

func (p Person) String() string{
	return fmt.Sprintf("Person{\"first\":%s, \"last\":%s, \"age\":%d}", p.First, p.Last, p.Age)
}

func main(){
	p1 := Person{"Murilo", "Carvalho", 36}
	p2 := Person{"Vegeta", "Prince", 44}
	p3 := Person{"Kakaroto", "Goku", 42}

	// Criando um JSON para enviar
	people := []Person{p1,p2,p3}

	byteSlice,err := json.Marshal(people)

	// Verifica se aconteceu algum erro no processo de codificação
	if err != nil {
		log.Fatalf("Erro ocorreu: %v", err)
	}

	// Converte o byte slice para uma string
	fmt.Println(string(byteSlice))
}
```

Para verificar o processo de retirar os dados e colocar dentro das estruturas de dados:

```go
package main

import (
	"encoding/json"
	"fmt"
	"log"
)

// Criando as estruturas que serão utilizadas

type Person struct{
	First string
	Last string
	Age int
}

func (p Person) String() string{
	return fmt.Sprintf("Person{\"first\":%s, \"last\":%s, \"age\":%d}", p.First, p.Last, p.Age)
}

func main(){
	p1 := Person{"Murilo", "Carvalho", 36}
	p2 := Person{"Vegeta", "Prince", 44}
	p3 := Person{"Kakaroto", "Goku", 42}

	// Criando um JSON para enviar
	people := []Person{p1,p2,p3}

	byteSlice,err := json.Marshal(people)

	// Verifica se aconteceu algum erro no processo de codificação
	if err != nil {
		log.Fatalf("Erro ocorreu: %v", err)
	}

	// Converte o byte slice para uma string
	fmt.Println(string(byteSlice))

	// Convertendo agora um array de objetos
	// O `` é utilizado para string multilinhas
	s := `[{"First":"Murilo","Last":"Carvalho","Age":36},{"First":"Vegeta","Last":"Price","Age":44},{"First":"Kakaroto","Last":"Goku","Age":42}]`

	bs := []byte(s)

	// Cria um conjunto de dados para armazenar a resposta
	var saida []Person
	
	err = json.Unmarshal(bs, &saida)

	// Verifica se algum erro aconteceu
	if err != nil {
		log.Fatalf("Erro ocorreu: %v", err)
	}

	fmt.Println(saida)

	// Passando por cada um dos objetos
	for i, p := range(saida){
		fmt.Println("Linha atual:", i)
		fmt.Println("Conteúdo:", p)
		fmt.Println("Nome:", p.First)
	}

}
```

---

O pacote `sort` traz algumas ferramentas que podem ser utilizadas para ordenar conjuntos de dados primitivos e definidos pelo usuário. Mais informações na documentação do pacote: https://pkg.go.dev/sort#pkg-overview. Verificar o pacote `bcrypt` para criptografia de projetos.

---

## 15. Paralelismo e Concorrência

Go aproveita múltiplos cores do processador. Paralelismo acontece quando o código pode ser executado em núcleos diferentes, sendo executados ao mesmo tempo. Concorrência é um padrão de desenvolvimento. Quando existe recursos de hardware, código concorrente pode ser executado em paralelo. Verificar a palestra de Rob Pike (https://www.youtube.com/watch?v=oV9rvDllKEg).

<iframe width="560" height="315" src="https://www.youtube.com/embed/oV9rvDllKEg?si=yiTbxmIYt4nzxLwX" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Para iniciar a compreensão deste conceito, vamos verificar este programa:

```go
package main

import "fmt"

func foo(){
	for i := 0; i < 10; i++ {
		fmt.Println("Foo:", i)
	}
}

func bar(){
	for i := 0; i < 10; i++ {
		fmt.Println("Bar:", i)
	}
}

func main(){
	foo()
	bar()
}
```


Ele vai produzir a saída:

```sh
Foo: 0
Foo: 1
Foo: 2
Foo: 3
Foo: 4
Foo: 5
Foo: 6
Foo: 7
Foo: 8
Foo: 9
Bar: 0
Bar: 1
Bar: 2
Bar: 3
Bar: 4
Bar: 5
Bar: 6
Bar: 7
Bar: 8
Bar: 9
```

Como esperado, uma vez que a função `foo()` foi invocada antes da função `bar()`. É possível utilizando o pacote `runtime` medir algumas das características do sistema que roda nosso programa:

```go
// Função para determinar a capacidade do nosso sistema operacional
func MedeAi(){
	fmt.Println("OS:", runtime.GOOS)
	fmt.Println("ARCH:", runtime.GOARCH)
	fmt.Println("CPUs:", runtime.NumCPU())
	fmt.Println("Goroutines:", runtime.NumGoroutine())
}
```

Quando desejamos utilizar uma Gorotine, que vai executar uma função de forma concorrente, utilizamos o operador `go` antes da chamada da função.

```go
package main

import (
	"fmt"
	"runtime"
)

func foo(){
	for i := 0; i < 10; i++ {
		fmt.Println("Foo:", i)
	}
}

func bar(){
	for i := 0; i < 10; i++ {
		fmt.Println("Bar:", i)
	}
}

// Função para determinar a capacidade do nosso sistema operacional
func MedeAi(){
	fmt.Println("OS:", runtime.GOOS)
	fmt.Println("ARCH:", runtime.GOARCH)
	fmt.Println("CPUs:", runtime.NumCPU())
	fmt.Println("Goroutines:", runtime.NumGoroutine())
}

func main(){
	MedeAi()
	go foo()
	go bar()
	MedeAi()
}
```

A saída do nosso programa será:

```sh
OS: windows
ARCH: amd64
CPUs: 6
Goroutines: 1
OS: windows
ARCH: amd64
CPUs: 6
Goroutines: 3
```

Repare que as saídas das funções não estão no nosso programa principal. Quando a função `main()` termina sua execução, todo o programa é encerrado. Existem algumas formas de sincronizar a execução das Gorotines.
