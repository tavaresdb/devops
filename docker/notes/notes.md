# Comandos úteis

## Registry
Repositório Docker: https://hub.docker.com/

## Criação do container com base na imagem
```bash
docker container run hello-world
```

## Listagem dos containers
```bash
docker container ls -a
```

## Parada do container
```bash
docker container stop :CONTAINER ID
```

## Inicialização do container
```bash
docker container start :CONTAINER ID
```

## Remoção do container
```bash
docker container rm :NAMES
docker container rm :CONTAINER ID
```

## Execução do container em modo interativo
```bash
docker container run -it ubuntu /bin/bash
```

## Execução do container em modo contínuo
```bash
docker container run -d -p 8080:80 ngnix
docker container run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=mongouser -e MONGO_INITDB_ROOT_PASSWORD=secret mongo
```

## Inspecionando o container
```bash
docker container inspect :CONTAINER ID
```

## Execução de procedimentos em um container em execução
```bash
docker container exec -it :CONTAINER ID /bin/bash
```

## Análise de logs do container
```bash
# Análise completa
docker container logs :CONTAINER ID

# Análise dos últimos 5 registros
docker container logs -n 5 :CONTAINER ID

# Análise contínua
docker container logs -f :CONTAINER ID
```

## Criação de imagem com Docker Commit (Prática não recomendável)
```bash
docker commit :CONTAINER ID joaotavares/my-ubuntu-custom:v1
```

## Criação de imagem com Dockerfile (Prática recomendável)
```bash
$ vi Dockerfile
..
FROM ubuntu
RUN apt-get update && \
    apt-get install curl --yes
:wq

docker image build -t joaotavares/my-ubuntu-file:v1 .
```

## Listagem das imagens
```bash
docker image ls
```

## Eliminação das imagens não utilizadas
```bash
docker image prune
```

## Envio de imagem para o repositório de imagens Docker, Registry
```bash
docker login
docker push joaotavares/my-ubuntu-file:v1
```

## Criação de uma rede
```bash
docker network create template_docker
```

## Listagem das redes
```bash
docker network ls
```

## Comunicação entre os containers
Caso os containers sejam iniciados sem a opção -p, não haverá conectividade com a rede devido a não publicação da porta do container no host. Uma vez que a rede foi criada via Docker Network, é possível fazer o vínculo da rede com o id dos containers desejados.

```bash
docker network connect template_netdocker :CONTAINER ID A
docker network connect template_netdocker :CONTAINER ID B
```

Obs.: Os containers podem ser iniciados especificando a rede criada. Por exemplo: docker container run -d --network template_netdocker ngnix.

## Volume
Containers são efêmeros, podendo ser iniciados ou removidos a qualquer momento. Caso um banco de dados seja conteneirizado, é importante que os dados não sejam perdidos, por isso a importância de trabalhar com volumes.

* Bind mount: Mapear diretório do host com o diretório do container
```bash
docker container run -it -v "$(pwd)/vol:/app" ubuntu /bin/bash
```

* Volume: O próprio docker gerencia o armazenamento;
```bash
docker volume create template_voldocker
docker volume ls
docker volume inspect template_voldocker
docker container run -it -v "template_voldocker:/app" ubuntu /bin/bash
```

* tmpfs: Armazenamento em memória.

### Opções
-d Executa o container em background
-i Executa o container em modo interativo
-t Habilita TTY
-p Realiza o bind entre a porta da máquina local e a porta no container
-e Define variável de ambiente