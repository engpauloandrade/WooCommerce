# Configuração de Ambiente de E-commerce com WordPress usando Docker

Este projeto configura um ambiente de e-commerce no WordPress com MySQL, utilizando Docker Desktop no Windows. Os dados são armazenados em volumes persistentes localizados em `C:\DockerOpenSource`.

## Pré-requisitos

- Docker Desktop instalado no Windows.

## Passos para Configuração

1. **Crie os arquivos de configuração**:
   - `docker-compose.yml` com o seguinte conteúdo:

```
 yaml
 version: '3.8'

 services:
 wordpress:
     image: wordpress:latest
     restart: always
     ports:
     - "80:80"
     environment:
     WORDPRESS_DB_HOST: db:3306
     WORDPRESS_DB_USER: wordpress
     WORDPRESS_DB_PASSWORD: wordpress
     WORDPRESS_DB_NAME: wordpress
     volumes:
     - wordpress_data:/var/www/html

 db:
     image: mysql:5.7
     restart: always
     environment:
     MYSQL_DATABASE: wordpress
     MYSQL_USER: wordpress
     MYSQL_PASSWORD: wordpress
     MYSQL_ROOT_PASSWORD: root_password
     volumes:
     - db_data:/var/lib/mysql

 volumes:
 wordpress_data:
     driver: local
     driver_opts:
     type: none
     device: "C:\\DockerOpenSource\\wordpress"
     o: bind
 db_data:
     driver: local
     driver_opts:
     type: none
     device: "C:\\DockerOpenSource\\db"
     o: bind
```

2. **Execute o Docker Compose**:
   - Abra o PowerShell ou Prompt de Comando.
   - Navegue até o diretório onde os arquivos foram salvos.
   - Execute o comando `docker-compose up -d`.

3. **Acesse seu site WordPress**:
   - Abra seu navegador e vá para `http://localhost`.

## Observações

- Para listar, execute `docker ps -a`.
- Para pausar o container, execute `docker stop id_do_seu_container`.
- Para parar e remover os containers, execute `docker-compose down`.


