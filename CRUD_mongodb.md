# CRUD em MongoDB

Informações retiradas do [site oficial](https://docs.mongodb.com/manual/crud/)

Nesse tutorial será ensinado como fazer um crud (Create, Read, Update, Delete) utilizando o gerenciador MongoDB. Para seguir este tutorial você deve ter o MongoDB instalado na sua máquina e rodando ele. Caso ainda não tenha, basta seguir o [tutorial de instalação](https://github.com/decoejz/cassandra-mongodb/blob/master/mongodb.md).

1) [Entendendo MongoDB](#1.-Entendendo-MongoDB)

    - [Criando uma Base de Dados](#Criando-uma-Base-de-Dados)
    - [Criando uma Coleção](#Criando-uma-Coleção)

2) [Inserindo Dados](#2.Inserindo-Dados)

    - [Adicionando um Dado](#Adicionando-um-Dado)
    - [Adicionando Vários Dado](#Adicionando-Vários-Dados)

3) [Lendo Dados](3.-Lendo-Dados)

    - [Todos os Dados](#Todos-os-Dados)
    - [Query](#Query)

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

Este comando é equivalente a query em SQL a seguir:

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

Equivalente em SQL a:

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

Equivalente em SQL a:

```SQL
SELECT donos FROM nomeDaColecao WHERE idade = 3
```

Para ter mais exemplos de query, entre no [site](https://docs.mongodb.com/manual/tutorial/query-documents/).