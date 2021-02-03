# lemp-docker-compose

Fully LEMP working environment for Docker compose.

## Pre-requisites

You must have docker desktop running on your computer. Follow instalation instructions from here:

https://docs.docker.com/desktop/

## Configuration

Check docker-compose.yml and change the volume for nginx and php-fpm where you have your code, by default it's serving from `src/` folder a default phpinfo() file.

## Get up & running

Just run `docker-compose up`