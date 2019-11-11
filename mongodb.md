# MongoDB

Tutorial para instalação do mongoDB

## Instalação

- Sistema Operacional: Ubuntu Server 16.04 Linux 64-bit x86
- Versão do MongoDB: 4.2

[1- Baixando a chave pública](#1--Baixando-a-chave-pública)

[2- Criando uma lista de arquivos](#2--Criando-uma-lista-de-arquivos)

[3- Recarregue o pacote local](#3--Recarregue-o-pacote-local)

[4- Instalando os pacotes do MongoDB](#4--Instalando-os-pacotes-do-MongoDB)

### 1- Baixando a chave pública

Para iniciar a instalação, de um terminal, importe a chave pública do MongoDB para sua máquina.

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
```

Você deverá receber um `OK` como confirmação.

> Caso receba um erro indicando `gnupg is not installed` você deve instalar ele:

> ```
> sudo apt-get install gnupg
> ```

> E por fim rodar o comando novamente.

### 2- Criando uma lista de arquivos

```
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
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