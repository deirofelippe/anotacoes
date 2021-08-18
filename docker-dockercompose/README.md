cria um container traves da imagem

criar grupo docker pra nao precisar rodar sudo
sudo addgroup docker
sudo usermod -aG docker $USER

- pra conseguir instalar pacotes dentro de um container linux, rode
apt update

- `adduser` pra criar outro usuario e nao usar o root
- `su` pra trocar de usuario

# Comandos
run --rm -d -p 8080:80 nginx
-d #deixa o bash livre, roda em segundo plano

docker info #mostra informacoes sobre o docker
docker images #lista as imagens baixadas
docker container list -a #lista todos os containers executado
docker ps -a
docker search <image> #procura a imagem
docker pull <image> #baixa a imagem

docker container run -it --name <name> <image> <command> #cria um container e roda de forma iterativa e mostrando o terminal
	docker container run -it ubuntu bash
	docker run -it ubuntu bash
docker stop <containder-id> #para o container
docker start <container-id> #inicia o container
docker exec -it <container-id> <command> #executa o container ja iniciado
	docker exec -it 34dc7d9e964c bash
	docker container start -ai 34dc7d9e964c

docker build -t <nome-pasta> <diretorio>
	docker build -t video .

docker rm $(docker ps -a -p) #lista o container id de todos os containers e remove todos
docker rm -f <container-id-ou-name> #mata o container sem precisar parar
docker rmi $(docker images -p) #lista a image id de todas as imagens e removo todas
docker rm <containder-id> #remove o container
docker rmi <image-id> #remove a imagem
docker run -it ubuntu bash --rm #quando sair do container, automaticamente ele é deletado

docker run -p 8080:80 nginx #roda um novo container, se o usuario acessar a porta 8080 na maquina normal, acessara a porta 80 do container
docker exec -it <container-name> <command> #executa um comando dentro de um container existente
	docker exec -it nginx bash

# Docker Compose

## Comandos

docker-compose ps #lista os containers
docker-compose up -d #executa o yaml
docker-compose up -d --build #rebuilda a imagem
docker-compose down #mata todos os containers

## Exemplo de uso

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

docker-compose up -d 

# Criar imagem

## Comandos

docker build -t <nome-imagem> <local-docker-file>
	docker build -t felippedeiro/teste-nginx .

docker run -d -p 8080:80 felippedeiro/teste-nginx

## Exemplo 

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
docker build -t felippedeiro/teste-nginx .

docker run -d -p 8080:80 felippedeiro/teste-nginx

# Docker Hub

Local onde armazena as imagens docker

docker login
docker push felippedeiro/teste-nginx





Automacao
	Git
	Docker
	Jenkins
	Zabbix
	Grafana

Orquestracao
	Kubernetes
	Nexus
	Puppet
	Ansible
	Terraform

Cloud
	Lambda
	EKS/ECS
	S3







remover do carrinho ou botao que vai pro carrinho



99taxi, easy taxi, nubank, ifood


Como o Google Funciona - Eric Schmidt 
Empresas Feitas Para Vencer - Collins Jim
Os Sete Hábitos das Pessoas Altamente Eficazes - Stephen Covey
Nada Easy - Tallis Gomes
Nova Economia - Diego Barreto
Organizações exponenciais - Salim
A startup enxuta - Eric Ries
Anti-fragil - Nassim Taleb
Do Mil ao Milhão - Thiago Nigro

- ter um time multiplica sua chance de sucesso, entao saiba contratar e saiba delegar
- delegar, se vc n é bom em organizar, contrate um CEO, contrate alguem que saiba fazer algo melhor que voce
- abrir uma empresa com um socio pra dividir os problemas
cada um tem uma funcao bem definida e tds se complementam: infra, dev, social media, marketing digital,
- consultoria de rh ou rh entrega os finalistas pro dono da empresa entrevistar, ou quem a pessoa vai trabalhar diretamente como um gerente.

