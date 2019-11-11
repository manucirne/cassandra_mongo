# MongoDB

Tutorial para instalação, conexão e desinstalação do mongoDB

Informações retiradas do [site oficial](https://docs.mongodb.com/manual/administration/install-on-linux/)

[Instalação](#Instalação)

[Conexão](#Conexão)

[Desintalação](#Desintalação)

---
## Instalação

- Sistema Operacional:
    - Ubuntu Server 16.04 (Xenial) Linux 64-bit x86
    - Ubuntu Server 18.04 (Bionic) Linux 64-bit x86*
- Versão do MongoDB: 4.2

*Existe apenas no passo 2 (Criando uma lista de arquivos) diferenças nos comandos executados.

[1- Baixando a chave pública](#1--Baixando-a-chave-pública)

[2- Criando uma lista de arquivos](#2--Criando-uma-lista-de-arquivos)

[3- Recarregue o pacote local](#3--Recarregue-o-pacote-local)

[4- Instalando os pacotes do MongoDB](#4--Instalando-os-pacotes-do-MongoDB)

---
### 1- Baixando a chave pública

Para iniciar a instalação, de um terminal, importe a chave pública do MongoDB para sua máquina.

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
```

Você deverá receber um `OK` como confirmação.

> Caso receba um erro indicando `gnupg is not installed` você deve instalar ele:
> 
> ```
> sudo apt-get install gnupg
> ```
> 
> E por fim rodar o comando novamente.

### 2- Criando uma lista de arquivos

Esse é o único comando desta etapa que tem diferença para as versões utilizadas.

- Ubuntu 16.04 (Xenial)
```
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
```

- Ubuntu 18.04 (Bionic)
```
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
```

### 3- Recarregue o pacote local

```
sudo apt-get update
```

### 4- Instalando os pacotes do MongoDB

Para instalar basta copiar o código abaixo:

```
sudo apt-get install -y mongodb-org
```

Com isso, o MongoDB esta instlado em sua máquina! Siga a próxima sessão para entender como conectar e utilizar este gerenciador.

---
## Conexão

Feita a instalação, agora é o momento de conectar sua máquina ao Mongo.

[1- Iniciando o MongoDB](#1--Iniciando-o-MongoDB)

[2- Finalizando o MongoDB](#2--Finalizando-o-MongoDB)

[3- Recomeçando o MongoDB](#3--Recomeçando-o-MongoDB)

[4- Conectando ao MongoDB](#3--Utilizando-o-MongoDB)

---
### 1- Iniciando o MongoDB

Para inicializar, basta copiar o comando abaixo:

```
sudo service mongod start
```

Mongod é o processo daemon para o MongoDB. Ele serve para os requerimentos feitos para o gerenciador tais como acessos e operações. 

Verifique se o processo iniciou com sucesso analisando o arquivo de log do MongoDB em `/var/log/mongodb/mongod.log`. A porta 27017 é a padrão de execução para o processo mongod.

### 2- Finalizando o MongoDB

```
sudo service mongod stop
```

### 3- Recomeçando o MongoDB

```
sudo service mongod restart
```

### 4- Conectando ao MongoDB

Com o MongoDB rodando em sua máquina, na porta 27017, basta executar o comando abaixo no seu terminal para se conectar.

```
mongo
```

Feito isso, o gerenciador pode ser utilizado conforme sua necessidade.

Uma vez conectado, para sair, basta digitar `exit`.

---
## Desintalação

Para desintalar completamente o MongoDB de sua máquina, primeiro [finalize o processo](#2--Finalizando-o-MongoDB) caso esteja sendo executado.

[1- Removendo os pacotes](#1--Removendo-os-pacotes)

[2- Removendo os diretórios de dados](#2--Removendo-os-diretórios-de-dados)

---
### 1- Removendo os pacotes

Remova os pacotes do MongoDB que foram instalados previamente

```
sudo apt-get purge mongodb-org*
```

### 2- Removendo os diretórios de dados

Remova a base de dados do MongoDB e os arquivos de log

```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```

Feito isso, o MongoDB foi desinstalado e excluido definitavamente. Caso queira reinstalar ele, basta seguir o passos no começo do tutorial - [Instalação](#Instalação).
