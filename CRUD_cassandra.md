# CRUD em Cassandra

Informações retiradas do [site oficial](http://cassandra.apache.org/doc/latest/getting_started/querying.html)

Nesse tutorial será ensinado como fazer um crud (Create, Read, Update, Delete) utilizando o shell de query (cqlsh) do cassandra. Para seguir este tutorial você deve ter o cassandra instalado na sua máquina. Caso ainda não tenha, basta seguir o [tutorial de instalação](https://github.com/decoejz/cassandra-mongodb/blob/master/cassandra.md).

1) [Entendendo Cassandra](#1-Entendendo-Cassandra)

    - [Criando um Keyspace](#Criando-Keyspace)
    - [Criando uma Tabela](#Criando-uma-Tabela)

2) [Inserindo Dados](#2-Inserindo-Dados)

3) [Lendo Dados](#3-Lendo-Dados)

    - [Todos os Dados](#Todos-os-Dados)
    - [Query](#Query)

4) [Alterando Dados](#4-Alterando-Dados)

5) [Deletando Informações](#5-Deletando-Informações)

---
## 1. Entendendo Cassandra

No Cassandra um conjunto de tabelas é chamado de keyspace. Como ele trabalha com clusters cada nó tem seus keyspace par que a organização entre eles aconteça corretamente.
O cqlsh usa uma linguagem muito semelhante ao mysql. Para entrar nesse shell basta utilizar o comando `cqlsh` na máquina que tem o cassandra instalado.

Para verificar as keyspaces existentes, utilize o comando `select * from system_schema.keyspaces;`.

Para verificar qual base de dados esta sendo utilizada, basta verificar o que está escrito a esquerda da linha de comando. Se o keyspace já está setado ele deve aparecer logo depois do cqlsh. É possível que nenhum keyspace esteja selecionado. Você pode trabalhar sem selecionar nenhum apenas acrescentando o nome do keyspace antes da tabela que deseja modificar com um ponto separando os nomes. Ex: `select * from nome_keyspace.nome_tabela;`.

Para verificar as tabelas existentes, utilize o comando `describe tables`. Se você estiver na keyspace desejada apenas as tabelas pertencentes a ela serão mostradas. Se você estiver fora de uma keyspace específica todas as tables serão mostradas com o keyspace à frente de seu nome.

### Criando Keyspace

Para criar uma keyspace, execute o comando com as alterações necessárias

```
CREATE  KEYSPACE IF NOT EXISTS nome_keyspace 
   WITH REPLICATION = { 
      'class' : 'SimpleStrategy', 'replication_factor' : N } | 
      'class' : 'NetworkTopologyStrategy', 
       'datacenter_name1' : N,
       'datacenter_name2' : M
   }
```

Você pode utilizar a classe 'SimpleStrategy' para utilização de replicas com as mesma configuração em todos os datacenters envolvidos, ou seja, a mesma quantidade de nós será utilizada em cada datacenter para replicas. A classe NetworkTopologyStrategy especifica o fator de replicas para cada datacenter separadamente. 
Veja um exemplo da criação de um keyspace com simplestrategy em um nó.

```
CREATE KEYSPACE nome_keyspace
  WITH REPLICATION = { 
   'class' : 'SimpleStrategy', 
   'replication_factor' : 1 
  };
```
Para trabalhar em apenas um keyspace execute o comando `use nome_keyspace`
Dessa forma, o keyspace aparecerá logo depois do cqlsh na linha de comando e não será necessário digitar o nome do keyspace para utilizar uma tabela pertencente a ele.

### Criando uma Tabela

A criação de uma tabela em cqlsh muito parecida com a sintaxe do mysql.
```
create table nome_tabela(parâmetro1 tipo PRIMARY KEY,
    parâmetro2 tipo,
    parâmetro3 tipo);
```
Não é necessário incluir uma PRIMARY KEY.
É possível inserir map, set e list, cahamadas de colection. Para isso o tipo da variável deve ser englobada com o nome da colection desejada. Ex: `map<text>`.

É possível encontrar os tipos aceitos na [documentação](http://cassandra.apache.org/doc/latest/cql/types.html) do cqlsh.

---
## 1. Inserindo Dados

Para adicionar dados a uma tabela utilize o comando a seguir:

```
insert into nome_tabela(parâmetro1, parâmetro2, parâmetro3) values ('nome', id, 'mensagem);
```

É possível inserir maps, sets e lists. Os parêmetros colection e podem ser inseridos e modificados por inteiro em um mesmo comando.

---
## 2. Lendo Dados

As operações de leitura retornam as informações contidas na tabela que esta sendo analisada. É possível pegar todos os dados de uma vez só ou criar queries para visualizar apenas os dados desejados.


### Todos os Dados de uma tabela

Para pegar todos os dados, basta digitar o comando `select * from nome_tabela`, lembrando que se o keyspace não estiver selecionado o nome da tabela deve ter o nome do keyspace com um ponto separando-os.

### Query

Existem muitas formas de filtrar os dados que se quer visualizar. A sintaxe é semelhante a utilizada em mysql. Alguns exemplos podem ser visualizados abaixo:

```
Select nome, idade from cliente where cidade = 'São Paulo';
```

Este comando retorna todos os nomes e idade de pessoas que moram em São Paulo


Outro exemplo:

```
select nome from cliente where idade > 18 and cidade = 'Rio de Janeiro';
```

Este comando retorna todos os clientes maiores de idade que moram no Rioj de Janeiro.

---
## 4. Alterando Dados

Alterar uma informação no cqlsh é muito semelhante ao mesmo comando para Mysql.

```
UPDATE Usuario
   SET bolsa = 1
   WHERE renda < 3000
     AND escola = 'publica';
```

## 5. Deletando Informações

Em cqlsh os dados podem ser deletados utilizando DELETE ou DROP. DELETE serve para deletar dados em tabelas e DROP serve para deletar estruturas como tabelas inteiras e keyspaces.


```
DELETE telefone FROM Usuario
 WHERE id = 30;
```

```
DROP TABLE Usuarios;
```

## 6. Fazendo Tudo ao Mesmo Tempo - Batch

em cqlsh é possível fazer várias operações ao mesmo tempo com o cmando Batch. Veja um exemplo abixo.

```
BEGIN BATCH
   INSERT INTO usuario (id, password, nome) VALUES (10, 'ch@ngem3b', 'Marilia');
   UPDATE usuario SET password = 'ps22dhds' WHERE userid = 10;
   INSERT INTO usuario (id, password) VALUES (30, 'kl3@ffl');
   DELETE nome FROM usuario WHERE id = 50;
APPLY BATCH;
```

Feito isso o CRUD esta completo. Esse tutorial é apenas uma introdução para o cqlsh do cassandra. Para obter mais informações sobre como ele funciona e possibilidade de métodos, entre no [site oficial](http://cassandra.apache.org/doc/latest/cql/index.html).
