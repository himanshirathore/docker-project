# docker-project
version: '3'

services:
  dbos:
    image: mysql:5.7
    volumes:
        - mysql_storage_new:/var/lib/mysql
    restart: always
    environment:
        MYSQL_ROOT_PASSWORD: rootpass
        MYSQL_USER: hena
        MYSQL_PASSWORD: redhat
        MYSQL_DATABASE: mydb

  wordpressos:
    image: wordpress:5.4.1-php7.3-apache
    restart: always
    depends_on:
        - dbos
    ports:
        - 8081:80
    environment:
        WORDPRESS_DB_HOST: dbos
        WORDPRESS_DB_USER: hena
        WORDPRESS_DB_PASSWORD: redhat
        WORDPRESS_DB_NAME: mydb
    volumes:
    - wp_storage_new:/var/www/html


volumes:
    wp_storage_new:
    mysql_storage_new:
