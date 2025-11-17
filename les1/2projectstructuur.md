# Project Structuur

Dit project maakt gebruik van een losse frontend en backend. Deze kunnen op verschillende servers/aparaten draaien. Het voordeel hiervan is dat je de backend kan gebruiken in meerdere projecten. (Gaan we ook doen).

Het doel van dit hoofdstuk is
* Het bouwen van ons project structuur
  * Dus een folder voor frontend en een folder voor de backend
* Docker

## Folder structuur
Maak een folder met de volgende structuur
```
todo-app/
   ├── backend/
   │   ├── php/
   │   │   ├── index.php
   │   │   └── api/
   │   ├── dockerfile
   │   └── docker-compose.yml
   │   
   └── README.md
```

## Docker Compose
Onze backend bestaat uit 3 images.
* PHP
* MySQL database
* phpmyadmin

```yml
version: '3.8'

services:
  php:
    build: .
    container_name: php_todo_app
    ports:
      - "8080:80"
    volumes:
      - ./php:/var/www/html
    depends_on:
      - db
    environment:
      MYSQL_HOST: db
      MYSQL_USER: root
      MYSQL_PASSWORD: rootpassword
      MYSQL_DATABASE: todo_app
  db:
    image: mysql:8.4
    container_name: mysql_todo_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: todo_app
    volumes:
      - mysql_data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    container_name: phpmyadmin_todo
    restart: always
    ports:
      - "8081:80"
    environment:
      PMA_HOST: db
      PMA_USER: root
      PMA_PASSWORD: rootpassword
    depends_on:
      - db

volumes:
  mysql_data:
```
Vergeet de docker file niet:
```dockerfile
FROM php:8.4-apache
RUN docker-php-ext-install mysqli pdo_mysql && docker-php-ext-enable mysqli
RUN a2enmod rewrite
```
Deze installeert mysqli en pdo_mysql. 

Start de container

---

Volgende stap: Het maken van de database en iets toevoegen.