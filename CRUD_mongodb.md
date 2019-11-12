# CRUD em MongoDB

Informações retiradas do [site oficial](https://docs.mongodb.com/manual/crud/)

Nesse tutorial será ensinado como fazer um crud (Create, Read, Update, Delete) utilizando o gerenciador MongoDB. Para seguir este tutorial você deve ter o MongoDB instalado na sua máquina e rodando ele. Caso ainda não tenha, basta seguir o [tutorial de instalação](https://github.com/decoejz/cassandra-mongodb/blob/master/mongodb.md).

1) [Entendendo MongoDB](#1.-Entendendo-MongoDB)

    - [Criando uma Base de Dados](#Criando-uma-Base-de-Dados)
    - [Criando uma Coleção](#Criando-uma-Coleção)

2) [Inserindo Dados](#2.Inserindo-Dados)

    - [Adicionando um Dado](#Adicionando-um-Dado)
    - [Adicionando Vários Dado](#Adicionando-Vários-Dados)

3) [Lendo Dados](#3.-Lendo-Dados)

    - [Todos os Dados](#Todos-os-Dados)
    - [Query](#Query)

4) [Alterando Dados](#4.Alterando-Dados)

    - [Alterar uma Informação](#Alterar-uma-Informação)
    - [Alterar Várias Informações](Alterar-Várias-Informações)
    - [Substituir uma Informação](Substituir-uma-Informação)

5) [Deletando Informações](#5.-Deletando-Informações)

    - [Deletar uma Informação](#Deletando-uma-Informação)
    - [Deletar Várias Informações](#Deletando-Diversas-Informações)

---
## 1. Entendendo MongoDB

MongoDB, assim como banco de dados relacionais tem diferentes bases de dados. Cada base de dados pode conter diversas tabelas, conhecidas em Mongo como colection (coleções).

Para verificar as bases de dados existentes, utilize o comando `show dbs`.

Para verificar qual base de dados esta sendo utilizada, utilize o comando `db`.

Para verificar as coleções existentes, utilize o comando `show collections` na base de dados desejada.

### Criando uma Base de Dados

Para criar uma nova base de dados, basta executar o comando

```
use nomeDaBase
```

Esse mesmo comando deve ser utilizado para utilizar uma base de dados já existente.

### Criando uma Coleção

Existem duas formas de adicionar uma nova coleção.

1) Será criada no momento em que um novo dados for inserido nela já com o nome desejado para a coleção. Caso a coleção já exista o dado será apenas armazenado. Vejá a sessão [inserindo dados](#2.Inserindo-Dados).

2) Caso tenha o desejo de especificar restrições, é possível criar uma nova coleção utilizando o método de criação do MongoDB. Para isso utilize o comando `db.createCollection(nomeDesejado, opções)`. Existem diversas opções que podem ser inseridas no momento de criação de uma coleção. Todas elas podem ser encontradas no [site](https://docs.mongodb.com/manual/reference/method/db.createCollection/#db.createCollection).

---
## 2. Inserindo Dados

Para adicionar dados a uma coleção, existem dois métodos. Um para adicionar apenas uma informação por vez e outro que adiciona diversos dados de uma vez só.

### Adicionando um Dado

Para adicionar um dado por vez, o comando utilizado é:

```
db.nomeDaColecao.insertOne(
    {
        nome: "lulu",
        idade: 5,
        donos: ["Maria"]
    }
)
```

### Adicionando Vários Dados

Para adicionar diversos dados de uma vez, a estrutura do comando é:

```
db.nomeDaColecao.insertMany(
    [
        {
            nome: "bidu",
            idade: 3,
            donos: ["Deco","Renato"]
        },
        {
            nome: "kef",
            idade: 6,
            donos: ["Manu"]
        }
    ]
)
```

---
## 3. Lendo Dados

As operações de leitura retornam as informações contidas na coleção que esta sendo analisada. É possível pegar todos os dados de uma vez só ou criar queries para visualizar apenas os dados desejados.

### Todos os Dados

Para pegar todos os dados, basta digitar o comando `db.nomeDaColecao.find()` que todas as informações contidas nesta coleção serão retornadas.

### Query

Para criar queries, a função utilizada é a mesma que a utilizada para pegar todos os dados porém com especificações no momento de execução. Alguns exemplos podem ser visualizados:

```
db.nomeDaColecao.find(
    {
        idade: 3
    }
)
```

Este comando retorna todos os valores cuja idade vale **3**. Ele é equivalente a query SQL a seguir:

```SQL
SELECT * FROM nomeDaColecao WHERE idade = 3
```

Outro exemplo:

```
db.nomeDaColecao.find(
    {
        idade: 3,
        nome: "bidu"
    }
)
```

Este comando retorna todas as ocasiões em que a idade vale **3** e o nome é **bidu**. A equivalência em SQL é:

```SQL
SELECT * FROM nomeDaColecao WHERE idade = 3 AND nome = "bidu"
```

Para conseguir um valor especifico:

```
db.nomeDaColecao.find(
    {
        idade: 3
    },
    {
        donos: 1
    }
)
```

Esse comando retorno o nome de todos os donos cuja idade vale **3**. A equivalência em SQL é:

```SQL
SELECT donos FROM nomeDaColecao WHERE idade = 3
```

Para ter mais exemplos de query, entre no [site](https://docs.mongodb.com/manual/tutorial/query-documents/).

---
## 4. Alterando Dados

Em mongo existem três formas possíveis de atualizar uma informação na base de dados. São elas [alterar uma informação](#Alterar-uma-Informação), [alterar várias informações](Alterar-Várias-Informações) ou [substituir uma informação](Substituir-uma-Informação)

### Alterar uma Informação

Para alterar uma informação, o comando abaixo deve ser executado. Podem haver filtros para saber exatamente qual a informação que deve ser alterada.

```
db.nomeDaColecao.updateOne(
    {
        nome: "bidu"
    },
    {
        $set: {idade:10}
    }
)
```

Esse comando irá alterar a idade para 10 anos, da primeira ocasião que aparecer o nome **bidu**.

### Alterar Várias Informações

O comando para alterar várias informações de uma vez é parecido com o de alterar apenas uma, mas ele alterará todas as ocasiões que o filtro apontar. Exemplo:

```
db.nomeDaColecao.updateMany(
    {
        idade:6
    },
    {
        $set: {nome:"Laila"}
    }
)
```

Esse comando altera todas as ocosiões da base de dados, cuja idade vale 6, para o nome **Laila**

### Substituir uma Informação

Caso deseja substituir completamente os valores de algum dado, essa opção pode ser a mais adequada.

```
db.nomeDaColecao.replaceOne(
    {
        idade:10
    },
    {
        nome:"jojo",
        idade:20,
        donos:["deco"]
    }
)
```

Esse comando altera todas as informações da primeira ocasião de ter algum item com valor de idade igual a 10 para os valores **jojo** como nome, idade de **20** e donos para **deco**.

Ele difere do método de [alterar apenas uma informação](#Alterar-uma-Informação) pois caso algum campo na sessão de substituição fique vazio, esse campo deixa de existir. Enquanto que no método de [alterar apenas uma informação](#Alterar-uma-Informação), basta colocar apenas o campo desejado de alteração e apenas ele será alterado, enquanto que os outros campos se mantêm constantes como estavam antes da ação.

---
## 5. Deletando Informações

Em mongo, existem duas possibilidades de deletar um dado. São elas [deletar uma Informação](#Deletando-uma-Informação) e [deletar várias informações](#Deletando-Diversas-Informações).

### Deletando uma Informação

Para apagar uma informação, o comando abaixo deve ser executado. Podem haver filtros para saber exatamente qual a informação que deve ser apagada.

```
db.nomeDaColecao.deleteOne(
    {
        idade:3
    }
)
```

Esse comando apagará a primeira ocasião que aparecer, cuja idade seja igual a **3**.

### Deletando Diversas Informações

O comando para apagar várias informações de uma vez é parecido com o de apagar apenas uma porém ao invés de apagar a primeira ocasião, ele apagará todas as ocorrências dela.

```
db.nomeDaColecao.deleteMany(
    {
        idade:6
    }
)
```

Feito isso o CRUD esta completo. Esse tutorial é apenas uma introdução para o gerenciador de banco de dados MongoDB. Para obter mais informações sobre como ele funciona e possibilidade de métodos, entre no [site oficial](https://docs.mongodb.com/manual/crud/).