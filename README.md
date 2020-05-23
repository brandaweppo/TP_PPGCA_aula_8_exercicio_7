# Técnicas de Programação/PPGCA
## Exercício 7 - Aula 8

###### 1. Criar diretório do  projeto chamado *solicitacoes-v1*
```
mkdir solicitacoes-v1
```
###### 2. Acessar diretório *solicitacoes-v1*
```
cd solicitacoes-v1/
```
###### 3. Criar arquivo *docker-compose*
```
fc > docker-compose.yml
```
###### 4. Editar arquivo *docker-compose*
```
version: '3'
services:
  db:
    image: postgres:9.6
```
###### 5. Listar arquivos dentro do projeto para confirmar se o arquivo foi criado
```
ls
```
###### 6. Verificar se há algo rodando
```
docker-compose ps
```
###### 7. Subir o arquivo *docker-compose* deixando-o em background
```
docker-compose up -d
```
###### 8. Listar imagens do docker e verificar se *postgres* está na lista
```
docker image ls
```
###### 9. Verificar se o container foi criado está listado, embora indicado pelo status *exit*
```
docker-compose ps
```
###### 10. Editar arquivo docker compose com variável de ambiente para que a máquina local possa acessar o banco de dados
```
    environment:
      POSTGRES_HOST_AUTH_METHOD: "trust"
```
###### 11. Derrubar container criado
```
docker-compose down
```
###### 12. Listar componentes do arquivo *docker-compose*
```
docker-compose ps
```
###### 13. Repetir comando para subir o arquivo *docker-compose* deixando-o em background
```
docker-compose up -d
```
###### 14. Listar componentes do arquivo *docker-compose* e verificar se status do container está *up*
```
docker-compose ps
```
###### 15. Acessar o que há no banco e listar quais os bancos de dados padronizados que vieram junto com a imagem
```
docker-compose exec db psql -U postgres -c '\l' 
```
###### 16. Criar a base de dados para a aplicação
###### 17. Criar um diretório chamado *scripts* para criar uma tabela e verificar se o que está sendo feito está correto
```
mkdir scripts
```
###### 18. Acessar diretório *scripts*
```
cd scripts/
```
###### 19. Criar arquivo *init*
```
fc > init.sql
```
###### 20. Criar arquivo *check*
```
fc > check.sql
```
###### 21. Voltar ao diretório anterior
```
cd ..
```
###### 22. Verificar se arquivos foram criados dentro do diretório *scripts*
```
ls scripts/
```
###### 23. Editar arquivo *init.sql* para criar um script de inicialização numa linguagem sql para criar a tabela e o banco de dados
```
CREATE DATABASE solicitacoes;
\c solicitacoes

CREATE TABLE pedidos (
	id serial not NULL,
	data TIMESTAMP not null DEFAULT CURRENT_TIMESTAMP,
	nome VARCHAR (100) not NULL,
	assunto VARCHAR (100) not NULL,
	mensagem VARCHAR (250) not NULL
);
```
###### 24. Editar arquivo *check.sql* para listar as bases, conectar com *solicitacoes* e ver como é formada a tabela de pedidos
```
\l
\c solicitacoes
\d pedidos
```
###### 25. Editar arquivo docker-compose para importar volumes
```
volumes:
  dados:

    volumes:
      - dados:/var/lib/postgresql/data
      - ./scripts:/scripts
      - ./scripts/init.sql:/docker-entrypoint-initdb.d/init.sql
```
###### 26. Verificar se o serviço está no ar, indicado pelo status *up*
```
docker-compose ps
```
###### 27. Baixar o container novamente
```
docker-compose down
```
###### 28. Repetir comando para subir o *docker-compose* deixando-o em background
```
docker-compose up -d
```
###### 29. Verificar se o serviço está ativo, indicado pelo status *up*
```
docker-compose ps
```
###### 30. Repetir o comando para listar as bases de dados e verificar se a base *solicitacoes* está listada
```
docker-compose exec db psql -U postgres -c '\l'
```
###### 31. Rodar arquivo que se chama *check* dentro do diretório correspondente
```
docker-compose exec db psql -U postgres -f /scripts/check.sql
```
###### 32. Criar um diretório chamado *web*
```
mkdir web
```
###### 33. Acessar diretório *web*
```
cd web/
```
###### 34. Criar arquivo *index.html*
```
fc > index.html
```
###### 35. Voltar ao diretório anterior
```
cd ..
```
###### 36. Listar diretórios para saber se foram criados
```
ls
```
###### 37. Editar arquivo docker-compose e configurar a parte web
```
  web:
    image: nginx:1.13
    volumes:
      - ./web:/usr/share/nginx/html
    ports:
      - 80:80
```
###### 38. Verificar se o sistema está ativo, identificado pelo status *up*
```
docker-compose ps
```
###### 39. Derrubar o serviço
```
docker-compose down
```
###### 40. Repetir comando para subir o *docker-compose* deixando-o em background
```
docker-compose up -d
```
###### 41. Verificar se os dois serviços estão ativos, identificado pelo status *up*
```
docker-compose ps
```
###### 42. Editar arquivo *index.html*
