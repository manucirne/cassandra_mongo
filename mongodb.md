# MongoDB

Tutorial para instalação do mongoDB

## Instalação

- Sistema Operacional: Ubuntu Server 18.04 Linux 64-bit x86
- Versão do MongoDB: 4.2

[1- Baixando a chave pública](#1--Baixando-a-chave-pública)

### 1- Baixando a chave pública

Para iniciar a instalação, de um terminal, importe a chave pública do MongoDB para sua máquina.

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
```

Você deverá receber um `OK` como confirmação.

> Caso receba um erro indicando `gnupg is not installed` você deve instalar ele:

> ```
> sudo apt install gnupg
> ```

> E por fim rodar o comando novamente.

