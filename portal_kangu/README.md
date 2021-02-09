# Buildar e executar container

Acessar a pasta portal_kangu pelo cmd, Powershell ou terminal

Caso não possua a imagem buildada **portal_kangu_web** ou tenha feito alguma alteração no arquivo portal\Dockerfile será necessário executar o seguinte comando:

```shell
...\docker\portal_kangu> docker-compose build
```

Ápos o termino do build será lançado algo parecido com:



```shell
    .
    .
    .
	
    Successfully built a5efbcf964da
    Successfully tagged portal_kangu_web:latest
```

Caso queira verificar se a imagem existe rodar o seguinte comando:

```shell
...\docker\portal_kangu> docker images
```

Na coluna **REPOSITORY** será possível ver a imagem gerada

Em seguida rodar o seguinte comando: 

```shell
...\docker\portal_kangu> docker-compose up -d
```

Onde será possível ver algo parecido com:

```shell
Creating portal_kangu ... done
```

Para verificar se o comando subiu o container iremos rodar o seguinte comando:

```shell
...\docker\portal_kangu> docker-compose ps
```

#Estrutura arquivos

Na pasta portal_kangu\portal iremos ver três arquivos:
1. default.conf
2. Dockerfile
3. php.ini

## default.conf
No arquivo default.conf temos três <VirtualHost *:80> onde inicialmente teremos portal, developer e trunk.

### VirtualHost
No VirtualHost portal seria a branch(pasta) para trabalhar. É a branch que nasce da **trunk**
No VirtualHost developer é a branch **developer**
No VirtualHost trunk é a branch **trunk**

## Dockerfile
Arquivo responsável por gerar a imagem

## php.ini
Arquivo de configuração do php

Na pasta **portal_kangu** temos o arquivo **docker-compose.yml** no item volumes, mais especificamente na linha 9, temos o "DE/PARA", onde apontamos para uma pasta que no caso do Windows configuramos para

```shell
C:\home\sistemas:/var/www/html
```

Caso queira configurar para Linux faremos a seguinte alteração nessa linha

```shell
/home/sistemas:/var/www/html
```

#Configuração hosts
No hosts do seu sistema será necessário fazer uma configuração no windows será necessário acessar através de um editor de texto (notepad) como administrador o caminho do arquivo é: 
```shell
C:\Windows\System32\drivers\etc\hosts
```
Para o sistema Linux

```shell
[vi | vim | nano] /etc/hosts
```
Incluir no arquivo a seguinte linha:

`127.0.0.1       dev.kangu.com.br trunk.kangu.com.br`

#Acessando a aplicação
Após as configurações executadas conforme mostrado nesse documento, iremos acessar pelo navegador: **dev.kangu.com.br** e **trunk.kangu.com.br**