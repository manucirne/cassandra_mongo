# Cassandra

Tutorial para instalação do gerenciador de bando de dados Cassandra

Informações retiradas do [site oficial](http://cassandra.apache.org/doc/latest/getting_started/index.html)

- [Instalação](#Instalação)

- [Conexão](#Conexão)

---
## Instalação

- Sistema Operacional:
    - Ubuntu Server 18.04 (Bionic) Linux 64-bit x86

Para fazer a instalação do Cassandra, é necessário ter *Oracle Java Standard Edition 8* ou *OpenJDK 8* e *Python 2.7* instalados em sua máquina.

Para baixar o OpenJDK no ubuntu basta digitar `sudo apt-get install openjdk-8-jre-headless`.

1) Adicione o repositório Apache do Cassandra em sua máquina:

```
echo "deb http://www.apache.org/dist/cassandra/debian 36x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
```

2) Adicione as chaves da Cassandra em sua máquina:

```
curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -
```

Você deverá receber um `OK` como confirmação.

> Caso receba o erro a seguir
> ```
> GPG error: http://www.apache.org 36x InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY CHAVE_XXXXXX
> ```
> Adicione a chave pública indicada pelo erro:
> ```
> sudo apt-key adv --keyserver pool.sks-keyservers.net --recv-key CHAVE_XXXXXX
> ```

3) Atualize o repositório:

```
sudo sudo apt update
```

4) Instale o Cassandra:

```
sudo apt install cassandra
```

---
## Conexão

Feita a instalação, agora é o momento de conectar sua máquina ao Cassandra.

1) [Iniciando o Cassandra](#1.-Iniciando-o-Cassandra)

2) [Finalizando o Cassandra](#2.-Finalizando-o-Cassandra)

<!--3) [Conectando ao MongoDB](#3.-Utilizando-ao-Cassandra)-->

---
### 1. Iniciando o Cassandra

Para inicializar, basta copiar o comando abaixo:

```
sudo service cassandra start
```

Para verificar que foi inicializado, digite `nodetool status`.

### 2. Finalizando o Cassandra

```
sudo service cassandra stop
```

<!--export CQLSH_NO_BUNDLED=true-->
<!--pip install cassandra-driver-->

<!--### 3. Conectando ao Cassandra

É necessário que o Cassandra esteja rodando em sua máquina, na porta 27017. Para isso basta seguir o passo [iniciando o MongoDB](#1.-Iniciando-o-MongoDB). Feito isso, bastaexecutar o comando abaixo no seu terminal para se conectar.

```
mongo
```

Feito isso, o gerenciador pode ser utilizado conforme sua necessidade.

Uma vez conectado, para sair, basta digitar `exit`.-->