# MongoDB VS Cassandra

Essa comparação visa mostrar quais as vantagens e desvantagens de cada um dos gerenciadores em questão. Além disso, apresentar em que aplicações e momentos um pode ser mais adequado que outros.

Vale enfatizar que nesse documento tem informações retiradas de diversos sites como [referência](#Referências), além de em alguns pontos ter a opinião dos escritores.

---
## Similaridades

Apesar de existirem diferenças entre essas duas tecnologias, elas têm algumas características iguais.

Ambos são baseados em estruturas de dados NoSQL. Modelo ideal para quantidades grandes de dados não estruturados.

As duas são open source, o que torna o acesso fácil para qualquer um que gostaria de criar um banco de dados.

Ambos tem diferentes linguagens que podem ser utilizadas para manusear eles, incluindo python, o que pode facilitar o desenvolvimento.

Por fim, existe suporte para as três principais distribuições de sistemas operacionais: Windows, Linux e macOS.

---
## Diferenças

Cada um dos gerenciadores tem suas vantagens e desvantagens. Elas serão analisadas a seguir. É importante enfatizar que cabe ao desenvolvedor saber quais as necessidades de sua aplicação para saber qual o gerenciador ideal.

### Alta Disponibilidade

Uma das questões que talvez sejá uma das mais importantes é a alta disponibilidade que o gerenciador tem. Caso seja uma aplicação com muitos acessos ao banco de dados e alta frequência, o ideal é buscar uma estrutura que garanta estabilidade nos momentos mais tranquilos de uso e também nos momentos com alta demanda. Se a aplicação for algo com poucos acessos ou baixa frequência, uma alta disponibilidade pode não ser referência como prioridade de projeto.

Quando se trata de **MongoDB** a opção do usuário é de configurar apenas um único nó como master e outros como slave. Caso o nó master de problema, um dos slaves automaticamente vira o master. Esse processo não é imediato e pode levar alguns minutos.

Já, ao tratar o **Cassandra**, a opção do usuário é de criar diversos nós masters, o que garante que caso algum falhe, outros estarão suprindo as necessidades imediatamente.

### Velocidade de Escrita

Essa analisa busca visualizar qual a velocidade de escrita de cada um dos gerenciadores.

Como o **MongoDB** tem apenas um nó master, sua velocidade de escrita pode ser pequena quando comparada com o **Cassandra** que tem diversos nós masters que podem ser utilizados para escrita.

Caso se tenha uma aplicação onde haverão muitas inserções, provavelmente o ideal é um gerenciador que faça essas ações de forma mais eficiente.

### Estrutura de Dados

Quando a estrutura de dados esta em análise, um banco de dados não relacional pode ter diversos formatos diferentes.

Em **MongoDB** a arquitetura é mais desestruturada. Nele, é permitido que se crie objetos da forma que quiser.

O **Cassandra** tem uma arquitetura mais similar com as de bancos de dados relacionais, apesar de não ser tão rigida quanto esses bancos.

### Linguagem

Os bancos de dados funcionam através de queries, que possibilitam busca, adicição e remoção de valores.

A linguagem do **Cassandra** (CQL) é muito similar a linguagem SQL, possibilitando inclusive que algumas queries em SQL funcionem em CQL.

Já o **MongoDB** tem sua própria linguagem. Para quem tem conhecimentos previos de SQL terá que aprender a lidar com ela. Não é uma linguagem complexa pois é bastante similar a um JSON, mas tem suas especificidades, o que pode ser um empecílio no momento de aprendizado.

### Implementação

O momento de instalação e implementação de um banco de dados pode não ser o principal foco no momento de decisão mas vale lembrar alguns pontos.

Como é possível perceber no [tutorial de instalação](https://github.com/decoejz/cassandra-mongodb/blob/master/mongodb.md) do **MongoDB**, apenas com simples passos é possível ter o banco de dados sendo executado e pronto para ser utilizado.

Já o **Cassandra** tem muito mais possibilidades de implementação e configurações disponíveis, o que pode ser um empecilho no momento de criação.

### Documentação

Ambos os gerenciadores tem sites próprios que contêm diversos tutoriais, desde instalação até CRUDs mais complexos.

Ao analisar eles, os tutoriais de **MongoDB** aparentam ser mais simples e fáceis de compreender do que os do **Cassandra**.

### Comentários Gerais

- **Cassandra** não tem suporte para indexações, as próprias queries resolverão esse problema. Já o **MongoDB** é mais preferível ter indexação já que caso não tenha, o documento inteiro deverá ser rodado para encontrar o desejado.

- **Cassandra** tem dependências de ter Java 8 e Python 2.7 instalados nas máquinas, enquanto que **MongoDB** não tem necessidade de nada específico.

---
### Referências

- [The Server Side](https://www.theserverside.com/tip/A-side-by-side-comparison-of-MongoDB-and-Cassandra-databases) - último acesso 14 de outubro de 2019

- [Panoplay Blog](https://blog.panoply.io/cassandra-vs-mongodb) - último acesso 14 de outubro de 2019