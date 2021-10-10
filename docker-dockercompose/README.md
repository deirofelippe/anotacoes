# Docker e Docker Compose

Instalação do [Docker](https://docs.docker.com/engine/install/ubuntu/) e do [Docker Compose](https://docs.docker.com/compose/install/#install-compose)

**Dica**: criar grupo docker pra nao precisar rodar sudo

```bash
sudo addgroup docker
sudo usermod -aG docker $USER
```

**Dica**: pra conseguir instalar pacotes dentro de um container linux, rode update do gerenciador de pacotes como `apt update` (linux debian e derivados) ou `apk update` (linux alpine)

## Conteudos

- [Docker](#docker)
   - [Comandos](#comandos-docker)
   - [Criar Imagem](#criar-imagem)
- [Docker Compose](#docker-compose)
   - [Comandos](#comandos-docker-compose)
   - [Exemplo](#exemplo-docker-compose)
- [Docker Hub](#docker-hub)

## Docker

### Comandos Docker

- `docker info`: mostra informacoes sobre o docker
- `docker images`: lista as imagens baixadas
- `docker ps -a`: lista todos os containers executado
- `docker search <imagem>`: procura a imagem
   - `docker search alpine`

- `docker pull <imagem>`: baixa a imagem
- `docker run -it --name <nome> <imagem> <comando>`: cria um container e roda de forma iterativa e mostrando o terminal
   - `docker run -it --name ubuntu-teste ubuntu bash`
   - `docker run -it ubuntu bash --rm`: quando sair do container, automaticamente ele é deletado
   - `docker run -d --rm -p 8080:80 nginx` #roda um novo container, se o usuario acessar a porta 8080 na maquina normal, acessara a porta 80 do container; quando o container for parado, automaticamente sera removido; executa sem deixar o terminal preso aos logs.

- `docker stop <containner-id>`: para o container
- `docker start <container-id>`: inicia o container que está parado
   - `docker start -ai 34dc7d9e964c`

- `docker exec -it <container-id-ou-nome> <comando>`: executa o container ja iniciado
   - `docker exec -it 34dc7d9e964c bash`
   - `docker exec -it nginx-teste bash`

- `docker rm $(docker ps -a -p)`: lista o container id de todos os containers e remove todos
- `docker rm -f <container-id-ou-name>`: mata o container sem precisar parar
- `docker rm <containder-id>`: remove o container
- `docker rmi $(docker images -p)`: lista a image id de todas as imagens e removo todas
- `docker rmi <imagem-id>`: remove a imagem

### Criar imagem

- `docker build -t <nome-imagem> <local-dockerfile>`
   - `docker build -t felippedeiro/teste-nginx .`

- `docker run -d -p 8080:80 felippedeiro/teste-nginx`

index.html

```xml
<!DOCTYPE html>
<html>
<head>
   <meta charset="utf-8">
   <title></title>
</head>
<body>
   <h1>Olá</h1>
</body>
</html>
```

Dockerfile

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
```

`docker build -t felippedeiro/teste-nginx .`

`docker run -d -p 8080:80 felippedeiro/teste-nginx`

## Docker Compose

### Comandos Docker Compose

- `docker-compose ps`: lista os containers
- `docker-compose up -d`: executa o yaml
- `docker-compose up -d --build`: rebuilda a imagem
- `docker-compose down`: mata todos os containers levantados pelo up

### Exemplo Docker Compose

./nodeapp/Dockerfile

```dockerfile
FROM node:15.14.0-alpine3.10
RUN apk add bash #linux alpine nao tem apt-get, tem apk
WORKDIR /usr/src/app
CMD ["tail","-f","/dev/null"] #nao deixa o container morrer
```

./nginx/Dockerfile

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
```

./docker-compose.yaml

```yaml
version: '3'
services: 
   web:
      build: ./nginx/
      ports:
         - 8080:80
      volumes:
         - ./nginx:/usr/share/nginx/html #o que mudar no './nginx', será replicado no '/user/share/nginx/html'
   nodeapp:
      build: ./nodeapp/
      ports:
         - 3000:3000
      volumes:
         - ./nodeapp:/usr/src/app
```

Rode `docker-compose up -d` no mesmo diretório que o `docker-compose.yaml`

## Docker Hub

Local onde armazena as imagens docker

- `docker login`
- `docker push felippedeiro/teste-nginx`
