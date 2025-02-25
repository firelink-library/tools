---
title: SQLite
sidebar_position: 1
slug: /sqlite
---

# SQLite

## 1. O que é SQLite?

O SQLite, segundo a definição da [documentação](https://www.sqlite.org/), é uma biblioteca implementada em C de um motor de base dados em SQL. Ele traz uma implementação pequena, rápida, alto-contida, de alta-confiança e com difersas funcionalidades da linguagem SQL.

O formato do arquivo que o SQLite utiliza é multi-plataforma (*cross-platform*) e retrocompatível entre versões. São um formato de arquivos para transferir conteúdos entre sistemas.

> *"SQLite is a C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine. The SQLite file format is stable, cross-platform, and backwards compatible and the developers pledge to keep it that way through the year 2050. SQLite database files are commonly used as containers to transfer rich content between systems [1](https://www.sqlite.org/aff_short.html) [2](https://www.sqlite.org/sqlar.html) [3](https://www.sqlite.org/appfileformat.html) and as a long-term archival format for data [4](https://www.sqlite.org/locrsf.html). There are over 1 trillion (1e12) SQLite databases in active use [5](https://www.sqlite.org/mostdeployed.html). SQLite source code is in the public-domain and is free to everyone to use for any purpose."* 

Legal, aqui temos uma definição do que é o SQLite, vinda do próprio site. Mas e porque utilizamos isso desta forma? Vamos estudar mais uns conceitos primeiro!

## 2. Como os dados podem ser modelados

A modelagem de dados tem um papel importante para compreender como os dados podem ser representados dentro do nosso sistema. Vamos avaliar essa afirmação e tentar compreender melhor ela.

> "Murilão, explica melhor o que esse negócio de modelar algo, isso ainda é meio estranho."

Quando estamos descrevendo alguma ação ou ainda quando estamos citando as características de algumas coisas, temos uma cituação em comum aqui: em ambas situações, estamos tentando representar um elemento abstrato, em que suas características vão permitir realizar uma sua representação.

> "Mas podemos deixar isso mais claro e um pouco mais longe do mundo abstrato."

Vamos lá, vamos pensar em um elemento que desejamos descrever e ver como podemos criar um ambiente para trabalhar com eles. Primeiro vamos tratar de um exemplo bastante comum, mas que serve para realizarmos o estudo do que desejamos!

Primeiro, vamos pensar em um elemento que eu espero que possa ser menos abstrato para todos! Um estudante!!

<img 
  src="https://cdn-icons-png.flaticon.com/512/257/257651.png"
  alt="I use Arch, BTW"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>

Como podemos descrever essa estudante? Podemos descrever ela por suas características físicas? Ou quem sabe podemos iniciar descrevendo algum dado de sua origem? Pessoal, algo que é interessante ficar claro: o que vamos modelar depende do contexto que desejamos representar. O que eu quero dizer com isso? Se estamos falando de estudantes, pode ser que modelar qual é o Pokémon favorito da primeira geração das pessoas, possa ser uma informação que podemos deixar passar.

| Característica     | O que ela Representa?                        | Tipo do Dado |
|--------------------|----------------------------------------------|--------------|
| Ano Entrada        | Ano que o estudante entrou na instituição    | Inteiro      |
| Nome               | Representa o nome de um estudante            | Texto        |
| Registro Acadêmico | Número que identifica o estudante no sistema | Texto        |
| Curso              | Curso do estudante                           | Texto        |


:::tip[Gerador de tabelas com Markdown]

Pessoal só por curiosidade, estou utilizando este gerador de tabelas para o Markdown: [Tables Generator](https://www.tablesgenerator.com/markdown_tables). Ajuda a editar elas mais rapidamente.

:::

Agora pessoal já temos algumas informações sobre como podemos deixar nosso estudante representado. Vale destacar aqui que mais informações podem ser utilizadas para representar estes estudantes, como características dos estudantes, informações de contato e o que fizer sentindo dentro do contexto que estiver modelando nosso problema. Verificando uma estrutura mais completa, podemos considerar:

| Característica     | Tipo do Dado |
|--------------------|--------------|
| Ano Entrada        | Inteiro      |
| Nome               | Texto        |
| Registro Acadêmico | Texto        |
| Curso              | Texto        |
| CPF/RG             | Texto        |
| Data Nascimento    | Data         |
| Endereço           | Texto        |
| Status Acadêmico   | Texto        |

Mas será que apenas com essas informações nós conseguimos representar nossos alunos? Será que para representar nosso sistema acadêmico, subindo aqui o escopo do que estamos modelando, não vamos precisar de mais elementos modelados? Vamos responder estas perguntas avançando mais um pouco nos conceitos que nós utilizamos!

:::tip[Para entender um pouco mais em vídeo]

Algumas sugestões de vídeos para compreender melhor os conceitos apresentados:

    <iframe width="560" height="315" src="https://www.youtube.com/embed/htOWhMc5N5M?si=Cp5cKZS-MGLY5qZS" title="Explicando o que são tabelas de dados nos bancos de dados" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
    <br/>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/wOD02sezmX8?si=YbqxviTKlaH38Jsn" title="Explicando o que são entidades" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
    <br/>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Bfm3Ms2cTg0?si=JgDbQBNazvgBWIFj" title="Explicando a origem dos bancos de dados" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
:::

## 3. Um pouco sobre Entidade e Relacionamentos

O `Modelo de Entidade-Relacionamento (MER)` é i,a ferra,enta conceitual utilizada na representação e organização dos dados de um sistema. Ele é utilizado nos bancos de dados relacionais, pois permite entender como os dados se relacionam entre si antes de realizar está implementação em um software de banco de dados.

Existem alguns conceitos importantes para conhecermos antes de iniciarmos nossa modelagem. São eles:
- `Entidade`: Representa um objeto ou conceito do mundo real que possui existência independente. Cada entidade é descrita por atributos (características). Exemplos: Estudante, Disciplina, Professor.
- `Atributo`: São as propriedades ou características de uma entidade ou relacionamento. Podem ter algumas variações: 
  - ***Simples***: Não pode ser dividido (ex.: CPF).
  - ***Composto***: Pode ser dividido em partes menores (ex.: Endereço → Rua, Cidade, CEP).
  - ***Multivalorado***: Pode ter mais de um valor (ex.: Telefones).
  - ***Derivado***: Pode ser calculado a partir de outros atributos (ex.: Idade a partir de Data_Nascimento).
- `Relacionamento`: Representa uma associação lógica entre duas ou mais entidades. Exemplos: Um Estudante cursa uma Disciplina; Um Professor ministra uma Turma.
- `Cardinalidade`: Define quantas instâncias de uma entidade podem se relacionar com instâncias de outra entidade. Tipos comuns:
  - ***1:1 (Um para Um)***: Ex.: Um estudante tem uma única matrícula.
  - ***1:N (Um para Muitos)***: Ex.: Um professor ministra várias turmas.
  - ***N:M (Muitos para Muitos)***: Ex.: Vários estudantes podem se matricular em várias disciplinas.

:::tip[Formas Normais em Bancos de Dados]

Aqui uma representação em vídeo sobre o que são formas normais de banco de dados:

    <iframe width="560" height="315" src="https://www.youtube.com/embed/Cj84bb04tio?si=ryFf_5Ti8w3YvkhO" title="Apresentando o processo de normalização de dados" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
    <br/>
   
:::

---

Para acompanhar nossos sistema, vamos dar uma olhada neste contexto aqui (eu dei uma forçada nela para ficar mais fácil de identificar algumas coisas):

Um cliente inicia a reunião explicando como o sistema deve funcionar:

> "Precisamos de um sistema para gerenciar nossas operações acadêmicas. Vou explicar como tudo funciona hoje, para que vocês possam desenvolver algo que atenda nossas necessidades."

1. Os Estudantes:

> "Temos muitos ***Estudantes*** aqui na universidade. Cada estudante tem um **Nome**, um **CPF** (que é único para cada um) e uma **Data Nascimento**. Esses são os dados básicos que precisamos armazenar. Um estudante pode se matricular em várias ***Disciplinas*** ao longo do curso. Por exemplo, um aluno pode estar cursando Matemática Avançada e Literatura Brasileira ao mesmo tempo. Precisamos que o sistema permita que um estudante se matricule em quantas disciplinas ele quiser, desde que cumpra os pré-requisitos."

2. As Disciplinas:

> "Cada ***Disciplina*** tem um **Nome** e uma **Carga Horaria**. Por exemplo, Matemática Avançada tem 60 horas, e Introdução à Programação tem 75 horas. As disciplinas são ofertadas semestralmente, e os estudantes podem escolher quais querem cursar. Ah, e cada disciplina é ministrada por um ***Professor***. Por exemplo, Matemática Avançada é ministrada pelo Professor Carlos, e Literatura Brasileira é ministrada pelo Professor João."

3. Os Professores:

> "Falando em professores, cada ***Professor*** tem um **Nome** e está vinculado a um **Departamento**. Por exemplo, o Professor Carlos é do Departamento de Ciências Exatas, e o Professor João é do Departamento de Letras. Um professor pode ministrar várias disciplinas. O Professor Carlos, por exemplo, ministra Matemática Avançada e Física Básica. Mas cada disciplina só pode ter um professor responsável. Não temos disciplinas com mais de um professor."

4. Os Relacionamentos:

> "Precisamos que o sistema reflita esses relacionamentos:

- Um ***Estudante*** pode se matricular em várias ***Disciplinas***.

- Um ***Professor*** pode ministrar várias ***Disciplinas***, mas cada ***Disciplina*** só pode ter um ***Professor***.

Além disso, o sistema precisa armazenar os dados básicos de cada entidade: **Nome**, **CPF**, **Data Nascimento** para os estudantes; **Nome** e **Carga Horaria** para as disciplinas; e **Nome** e **Departamento** para os professores."

5. Exemplo Prático:

> "Vou dar um exemplo prático para ficar mais claro. A Ana é uma estudante que acabou de se matricular. Ela escolheu três disciplinas: Matemática Avançada, Literatura Brasileira e Introdução à Programação. O Professor Carlos ministra Matemática Avançada, e o Professor João ministra Literatura Brasileira. Já Introdução à Programação é ministrada pelo Professor Maria, do Departamento de Computação. O sistema precisa permitir que a Ana visualize suas disciplinas e os professores responsáveis por cada uma, assim como os professores precisam ver quais estudantes estão matriculados em suas disciplinas."

6. Requisitos Finais:

> "Resumindo, o sistema deve:"

- Cadastrar Estudantes, Disciplinas e Professores com seus respectivos atributos.

- Permitir que estudantes se matriculem em várias disciplinas.

- Permitir que professores ministrem várias disciplinas, mas cada disciplina só pode ter um professor.

- Ser capaz de gerar relatórios, como a lista de estudantes matriculados em uma disciplina ou as disciplinas ministradas por um professor.

Agora vamos ver como podemos utilizar um Diagrama de Entidade-Relacionamento (DER) para representar este nosso sistema. Para realizar está representação, vamos utilizar como convenção:

- Entidades são retângulos.
- Relacionamentos são losangos.
- Atributos são elipses.
- Linhas conectam entidades a relacionamentos, com cardinalidades indicadas (ex.: 1..\*, \*..\*).

No nosso exemplo:

```sh
[Estudante] * ----(Matricula)---- * [Disciplina]  
                                          *
                                          |  
                                      (Ministra)  
                                          | 
                                          1 
                                     [Professor]  
```

:::tip[Diagrama Entidade-Relacionamento]

Mais alguns complementos sobre como utilizar estes diagramas:

    <iframe width="560" height="315" src="https://www.youtube.com/embed/XCkd27GtZoM?si=fd-ec_mOtaBAzZmR" title="Diagrama Entidade-Relacionamento" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
    <br/>
   
:::

## 4. Chen?

A notação de Chen é uma forma de representar modelos de entidades e relacionamentos (ER) na engenharia de software e, em especial, na concepção de bancos de dados. Criada por Peter Chen em 1976, essa notação se popularizou por oferecer uma maneira clara de visualizar como os dados se inter-relacionam em um sistema. O diagrama resultante é composto por retângulos que representam entidades, losangos para relacionamentos e elipses para atributos, proporcionando uma visão estruturada das informações e facilitando a análise e o desenho de bancos de dados.

Para utilizar a notação de Chen, primeiramente identificam-se as entidades principais do domínio do problema, que podem ser, por exemplo, pessoas, produtos ou departamentos. Em seguida, definem-se os relacionamentos, que indicam como essas entidades se conectam. Um relacionamento pode ser de um para um (1:1), de um para muitos (1:N) ou de muitos para muitos (M:N). Já os atributos descrevem características das entidades ou dos relacionamentos, como nome, data de criação ou valores numéricos. Além disso, é possível indicar chaves primárias, chaves estrangeiras e outras restrições, enriquecendo o modelo e permitindo que eventuais ambiguidades sejam esclarecidas antes da implementação no banco de dados.

A adoção da notação de Chen traz diversos benefícios, por ser visualmente intuitiva, ela promove uma comunicação eficaz entre os membros da equipe e outros stakeholders, como clientes e gerentes de projeto, tornando as discussões sobre requisitos e estrutura de dados mais ágeis e claras. A diagramação prévia em notação de Chen auxilia a detectar inconsistências e redundâncias no modelo de dados, o que potencialmente reduz custos e esforços de correção em etapas posteriores do projeto.

:::tip[Uma represenção em vídeo]

Recomendo muito verificar esse vídeo pessoal, ele traz um resumo do que abordamos até aqui:

    <iframe width="560" height="315" src="https://www.youtube.com/embed/LowjDtiNlk4?si=Si4T35OnHlEnH3kk" title="Diagrama Entidade-Relacionamento" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
    <br/>
   
:::

## 5. Enfim, algo estruturado

Beleza, falamos um monte, mas vamos fazer? Vamos colocar nosso sistema no ar, colocando nossas tabelas ... caramba! Esquecemos de colocar nossas tabelas! Vamos rapidamente escrever elas aqui, depois vamos utilizar o SQL para colocar elas no nosso banco de dados SQLite.

| Tabela - Estudante | Atributo | Tipo do Dado |
| --- |:---:|:---:|
| | nome | texto |
| | cpf | texto |
| | data_nascimento | data |

| Tabela - Disciplina | Atributo | Tipo do Dado |
| --- |:---:|:---:|
| | nome | texto |
| | carga_horaria | texto |

| Tabela - Professor | Atributo | Tipo do Dado |
| --- |:---:|:---:|
| | nome | texto |
| | departamento | texto |


:::note[Pode ser feito de muitas outras formas]

Pessoal acho que nunca é demais chamar a atenção para este ponto: está modelagem e implementação podem ser realizadas de outras formas. Sugiro fortemente que vocês modifiquem esses elementos e façam tais alterações, para ver como o sistema se comporta.

:::

Legal, temos nosso primeiro projeto de tabelas 📅! Agora vamos utilizar o SQL para criar elas!

> Mas Murilão eu não sei SQL!

Calma! Eu vou explicando os comandos conforme formos utilizando eles, aqui em baixo tem mais alguns links caso você deseje estudar mais!

:::tip[Para conhecer mais SQL]

Aqui algumas recomendações para estudar SQL:

- Essa é da Lika (vou adicionar o Github dela aqui): [SQL Murder Mystery](https://mystery.knightlab.com/)
- Recomendo tanto o material do [Luke Barousse](https://www.youtube.com/@LukeBarousse) quanto do [Alex The Analyst
](https://www.youtube.com/@AlexTheAnalyst)

    <iframe width="560" height="315" src="https://www.youtube.com/embed/7mz73uXD9DA?si=TacHMY7iAJLIuSme" title="SQL for Data Analytics - Learn SQL in 4 Hours" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
    <br/>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/OT1RErkfLNQ?si=nAs2IVxxgUtu4Kno" title="Learn SQL Beginner to Advanced in Under 4 Hours" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
    <br/>

:::

Quando trabalhando com SQLite, particularmente gosto de utilizar o [DBeaver](https://dbeaver.io/) para criar e manipular o arquivo do banco. Uma alternativa para não precisar instalar nada no computador, é utilizar o [SQLite Online](https://sqliteonline.com/). 
Para criar nossas tabelas:

```sql
CREATE TABLE Estudante(
	nome VARCHAR(100) NOT NULL,
  	cpf VARCHAR(15) PRIMARY KEY,
  	data_nascimento DATE
);

CREATE TABLE Disciplina(
	nome VARCHAR(100) NOT NULL,
  	carga_horaria INTEGER NOT NULL,
  	id INTEGER PRIMARY KEy AUTOINCREMENT
);


CREATE TABLE Professor(
	nome VARCHAR(100) NOT NULL,
  	departamento VARCHAR(100) NOT NULL,
  	id INTEGER PRIMARY KEy AUTOINCREMENT
);
```

Vamos por partes compreender cada um destes elementos:

- ***Estudante***:
  - `CREATE TABLE Estudante`: Inicia a criação de uma tabela chamada Estudante no banco de dados.
  - `nome VARCHAR(100) NOT NULL`: nome é o nome da coluna. VARCHAR(100) indica que a coluna armazenará texto com até 100 caracteres (em SQLite, apesar do tipo VARCHAR, internamente o armazenamento é tratado como TEXT, mas a declaração respeita a sintaxe SQL). NOT NULL significa que esse campo não pode receber valores vazios (NULL), obrigando o preenchimento do nome do estudante ao inserir um registro.
  - `cpf VARCHAR(15) PRIMARY KEY`: cpf é a coluna para armazenar o CPF do estudante. VARCHAR(15) indica um campo de texto com até 15 caracteres (suficiente para representar o formato do CPF, incluindo possíveis traços ou pontos, se necessário). PRIMARY KEY define que essa coluna é a chave primária da tabela, ou seja, cada valor de CPF deve ser único e não pode ser nulo. É por esse campo que os registros serão identificados de forma única.
  - `data_nascimento DATE`: data_nascimento é a coluna responsável por armazenar a data de nascimento do estudante. DATE indica o tipo de dado de data. Em SQLite, embora o tipo DATE possa ser armazenado como texto, é convencionado que esse campo representará uma data.

- ***Disciplina***:
  - `CREATE TABLE Disciplina`: Cria a tabela Disciplina no banco de dados.
  - `nome VARCHAR(100) NOT NULL`: Define a coluna nome para armazenar o nome da disciplina, com até 100 caracteres de texto e que não pode ser nulo (NOT NULL).
  - `carga_horaria INTEGER NOT NULL`: carga_horaria é uma coluna do tipo numérico (INTEGER), usada para guardar a quantidade de horas de aula ou estudo que a disciplina exige. Também está definida como NOT NULL, ou seja, não pode ficar sem valor.
  - `id INTEGER PRIMARY KEY AUTOINCREMENT`: id é do tipo inteiro (INTEGER). PRIMARY KEY indica que esta coluna é a chave primária da tabela, garantindo que cada registro em Disciplina seja identificado exclusivamente por esse campo. AUTOINCREMENT faz com que o valor de id seja gerado e incrementado automaticamente pelo banco de dados sempre que um novo registro for inserido. **Observação**: em SQLite, para utilizar o autoincremento de forma apropriada, a coluna com PRIMARY KEY AUTOINCREMENT deve ser do tipo INTEGER.

- ***Professor***:
  - `CREATE TABLE Professor`: Cria a tabela Professor.
  - `nome VARCHAR(100) NOT NULL`: Coluna para o nome do professor, até 100 caracteres, não pode ser nula.
  - `departamento VARCHAR(100) NOT NULL`: Coluna que indica o departamento ao qual o professor está vinculado, também não pode ser nula.
  - `id INTEGER PRIMARY KEY AUTOINCREMENT`: Coluna inteira que serve como chave primária da tabela, sendo gerada automaticamente (incrementada a cada novo registro).

Ufa! Criamos nossas tabelas! Agora, este arquivo com os nossos dados pode ser baixado o utilizado para acessarmos suas informações. É importante ressaltar um ponto aqui, ainda não temos dados dentro do nosso banco, apenas a sua estrutura.

:::tip[Para saber mais]

Pessoal está palestra do Richard Hipp traz muitos detalhes de como as informações são armazenadas em base de dados SQLite.

  <iframe width="560" height="315" src="https://www.youtube.com/embed/ZSKLA81tBis?si=PvM1fV7KP7u1stAz" title="SQLite: How it works, by Richard Hipp" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
  <br/>

:::

## 6. O tal do CRUD

Boa, temos até aqui nosso banco e nossas tabelas, vamos falar agora sobre as operações que podemos fazer com eles.

<img 
  src="https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_99257e2c4240770e6b4bdd406d943ac8.png"
  alt="I have the data!! Meme."
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '60vh',
    marginRight: 'auto'
  }} 
/>
<br/>

As operações de CRUD representam as quatro ações fundamentais para manipulação de dados em um sistema ou banco de dados. A sigla deriva do inglês *Create* (criar), *Read* (ler), *Update* (atualizar) e *Delete* (excluir). São elas:

1. ***Create (Criar)***: Incluir novos registros no sistema ou banco de dados.
2. ***Read (Ler)***: Consultar e recuperar dados existentes.
3. ***Update (Atualizar)***: Modificar informações de registros já existentes.
4. ***Delete (Excluir)***: Remover registros que não são mais necessários.


Essas operações são importantes pois dão a base para que um sistema possa não só armazenar dados, mas também manter essas informações atualizadas e acessíveis. Isso garante o ciclo de vida completo de um dado dentro de uma aplicação, indo desde a inserção de novas informações até a exclusão de dados obsoletos. Além disso, o CRUD é a base para a maioria das funcionalidades de sistemas de gestão, sites de comércio eletrônico, plataformas de redes sociais e qualquer aplicação que precise gerenciar dados de forma estruturada.

Vamos ver um pouco mais sobre como podemos fazer cada um destas operações.

### 6.1 Create (Criar)

A operação Create é usada para adicionar novos registros ou dados a uma tabela ou coleção. No contexto de um banco de dados, isso é feito com o comando INSERT. Exemplo em SQL:

```sql
INSERT INTO Estudante (nome, cpf, data_nascimento) 
VALUES ('João Silva', '123.456.789-00', '2000-01-01');
```

### 6.2 Read (Ler)

A operação Read é usada para recuperar ou consultar dados existentes em uma tabela ou coleção. No contexto de um banco de dados, isso é feito com o comando SELECT. Exemplo em SQL:

```sql
SELECT * FROM Estudante WHERE cpf = '123.456.789-00';
```

### 6.3 Update (Atualizar)

A operação Update é usada para modificar dados existentes em uma tabela ou coleção. No contexto de um banco de dados, isso é feito com o comando UPDATE. Exemplo em SQL:

```sql
UPDATE Estudante 
SET nome = 'João da Silva' 
WHERE cpf = '123.456.789-00';
```

### 6.4 Delete (Excluir)

A operação Delete é usada para remover registros ou dados de uma tabela ou coleção. No contexto de um banco de dados, isso é feito com o comando DELETE. Exemplo em SQL:

```sql
DELETE FROM Estudante 
WHERE cpf = '123.456.789-00';
```

---

### 6.5 Pensando no nossos dados

Agora vamos pensar no nosso conjunto de dados. Vamos inserir alguns dados nas tabelas para consultarmos posteriormente. Fica como desafio, avaliar os comandos abaixo e verificar o que eles vão fazer. Tente fazer isso antes de executar os comandos. Depois de realizada sua implementação, tente verificar se ele fez o que você imaginou para cada um deles.

```SQL
INSERT INTO Disciplina (nome, carga_horaria) VALUES
('Matemática', 60),
('Português', 50),
('História', 40),
('Geografia', 40),
('Ciências', 50);

INSERT INTO Estudante (nome, cpf, data_nascimento) VALUES
('Ana Silva', '111.222.333-44', '2005-03-15'),
('Bruno Oliveira', '222.333.444-55', '2004-07-22'),
('Carla Santos', '333.444.555-66', '2006-01-10'),
('Daniel Costa', '444.555.666-77', '2005-11-30'),
('Eduarda Pereira', '555.666.777-88', '2004-09-05'),
('Fernando Almeida', '666.777.888-99', '2003-05-12'),
('Gabriela Rocha', '777.888.999-00', '2004-08-19'),
('Hugo Martins', '888.999.000-11', '2005-02-25'),
('Isabela Lima', '999.000.111-22', '2006-06-30'),
('João Vitor Souza', '000.111.222-33', '2003-12-05'),
('Karina Fernandes', '111.222.333-43', '2004-04-18'),
('Lucas Gonçalves', '222.333.444-54', '2005-09-22'),
('Mariana Castro', '333.444.555-65', '2006-03-14'),
('Nicolas Ribeiro', '444.555.666-76', '2003-11-08'),
('Olivia Duarte', '555.666.777-87', '2004-07-01');

INSERT INTO Professor (nome, departamento) VALUES
('Carlos Mendes', 'Matemática'),
('Patrícia Alves', 'Letras'),
('Ricardo Fernandes', 'História'),
('Sandra Oliveira', 'Ciências'),
('Prof. Carvalho', 'Ciências'),
('Utônio', 'Ciências'),
('Senku Ichigame', 'Ciências'),
('Cutty Flam Franky', 'Matemática'),
('Nico Robin', 'Geografia')
('Tiago Costa', 'Geografia');
```

:::tip[Para ver em vídeo mais informações]

  <iframe width="560" height="315" src="https://www.youtube.com/embed/jkEr7vcsjWY?si=eAxFZjLDyly79XTq" title="Operações CRUD no SQL Server - Introdução ao CRUD" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
  <br/>

:::

## 7. Implementando em Python

## 8. Agora vamos dar uma melhorada

## 9. Revisão tudo

## 10. Para saber mais

Pessoal aqui eu estou deixando uma sequencia de vídeos que eu acho que são recursos interessantes para aprender SQL e como utilizar ele.

> Nossa Murilão, eu estava acompanhando os commits e vi que esse material ficou pronto antes! Por que isso?

Eu fui montando ele conforme fui vendo alguns recursos que achei bastante interessantes, por isso ele foi nascendo conforme fui encontrando material que eu achei que seria interessante!

<iframe width="560" height="315" src="https://www.youtube.com/embed/zsjvFFKOm3c?si=RNK71PM1fzpWGjwu" title="SQL Explained in 100 Seconds" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/xiUTqnI6xk8?si=jr81l1Hn7HlczSpA" title="you need to learn SQL RIGHT NOW!! (SQL Tutorial for Beginners)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/yMqldbY2AAg?si=JzloaluW_iVexHIQ" title="Roadmap for Learning SQL" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/_vxobA36UN4?si=MnglUWioxm9_ituX" title="Learn 12 Basic SQL Concepts in 15 Minutes (project files included!)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" style={{display:"block", marginLeft:"auto", marginRight:"auto"}} allowfullscreen></iframe>
<br/>