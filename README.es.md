# Configuración de docker compose para PHP, mginx, PHP-FPM, MySQL, PostgreSQL, Composer y Symfony

> Configuración de Docker Compose para ejecutar PHP, mginx, PHP-FPM, MySQL, PostgreSQL, Composer y Symfony

- PHP 7.4.14
- nginx 1.18
- MySQL 8.0.23
- PostgreSQL 13.1

![GitHub](https://img.shields.io/github/license/mbelchin/docker-php-nginx-mysql-postgres-composer.svg)
![GitHub release](https://img.shields.io/github/release/mbelchin/docker-php-nginx-mysql-postgres-composer.svg)

[![Twitter](https://img.shields.io/twitter/url/https/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2Fmbelchin%2Fdocker-php-nginx-mysql-postgres-composer&hashtags=docker,docker-compose,php,php7,nginx,mysql,mysql8,postgres,postgres13,composer,symfony)

*Lee esta información en otros idiomas: [English](README.md), [Español](README.es.md).*

## Introducción

Esta configuración de Docker compose te permite ejecutar PHP 7.4 con nginx 1.18, PHP-FPM, MySQL 8.0.23, PostgreSQL 13.1, Composer y Symfony.

Expone estos 4 servicios:

- nginx
- php-fpm
- mysql
- postgres

Para conocer todas las extensiones habilitadas para PHP puedes ejecutar el comand `docker-compose up` y visitar esta URL: http://localhost/ en tu navegador, podrás comprobar la información de PHP con todo detalle.

Por defecto, PHP tiene habilitadas las extensiones **pdo_mysql**, **pdo_pgsql** y **Xdebug**.

La extesión UUID también está disponible para PostgreSQL.

nginx inluye una configuración por defecto básica para Symfony 5.

Composer se ejecuta cuando se incian los contenedores para instalar las librerías externas. Más información: https://getcomposer.org

El comando Symfony tambbién está disponible para facilitarte el desarrollo. Más información: https://symfony.com/download


## Requisitos previos

Debes tener docker instalado y funcionando en tu ordenador. Sigue las instrucciones aquí:

https://docs.docker.com/desktop/


## Como utilizarlo

### Iniciar docker compose

Clona este repositorio o descargalo en tu ordenador.

Simplemente ejecuta `docker-compose up`

Por defecto, nginx está disponible en `http://localhost:80`, PostgreSQL en `http://localhost:5432` y MySQL en `http://localhost:3306`

### Usar nginx

Puedes ejecutar comandos para nginx cuando lo necesites, así:

`docker-compose exec nginx nginx -v`

### Usar Composer

Puedes ejectuar comandos de composer así:

`docker-compose run composer <comando-composer>`

`docker-compose run composer -V`

### Usar Symfony

Ejecutar comandos de symfony, así:

`docker-compose exec php-fpm symfony <comando-symfony>`

Por ejemplo, puedes comprobar los requisitos mínimos de symfony:

`docker-compose exec php-fpm symfony check:req`

### Usar PHP

Ejecuta comands de PHP de este modo:

`docker-compose exec php-fpm php -v`

### Usar PostgreSQL

Puedes consultar la versión de PostreSQL ejecutando:

`docker-compose exec postgres postgres -V`

Y trabajar con tus bases de datos así:

`docker-compose exec postgres psql -d testdb -U myuser`

### Usar MySQL

Puedes consultar la versión de MySQL ejecutando:

`docker-compose exec mysql mysql -V`

Y trabajar con tus bases de datos así:

`docker-compose exec mysql mysql -u root -pmyrootpassword`



## Configuración

### Configurando volúmenes

Por defecto, cuando ejecutas `docker-compose up` monta la carpeta `src/` como un volumen. Será el directorio utilizado por defecto para servir to código fuente.

Comprueba el fichero `docker-compose.yml` y cambia los volúmenes para nginx y php-fpm para que monte el directorio donde se encuentra tu código.

Puedes cambiar `./src/` en `volumes:` a cualquier otro directorio en tu sistema.

```
volumes:
  - ./src/:/var/www/
```

Por ejemplo:

```
volumes:
  - ../mi-proyecto-symfony/:/var/www/
```

### Configurando las bases de datos

Por defecto, la configuración de `docker-compose.yml` ejecuta las dos bases de datos, tanto MySQL como PostgreSQL.

Si solo quieres o necesitas una única base de datos puedes comentar el código (o eliminarlo) de la base de datos con la que no quieres trabjar en el fichero `docker-compose.yml`.

El fichero `.env` almacena la información sensible de user & password para poder conectar con las bases de datos.

Modifica el fichero `.env` de acuerdo a tus necesidades.

### Configurando PHP

Puedes habilitar/dehabilitar cualquier directiva de PHP simplemente editando estos ficheros:

`./php-fpm/conf.d/php.ini` o `./php-fpm/conf.d/xdebug.ini`

