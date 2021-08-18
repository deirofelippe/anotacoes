docker-compose up
docker exec -it exemplo_nodeapp_1 bash
	yarn install
	yarn start

acesse a url 'localhost:8080' pra acessar o container 'nodeapp' atraves do proxy reverso feito pelo nginx no container 'web'

acesse a url 'localhost:9000' pra acessar o pgadmin4 atraves do container 'pgadmin'

docker-compose down