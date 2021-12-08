# Symfony 5 Docker-Development-Stack
This is a lightweight stack based on Alpine Linux for running Symfony 5 into Docker containers using docker compose.

<!-- [![Build Status](https://travis-ci.com/coloso/symfony-docker.svg?branch=master)](https://travis-ci.org/coloso/symfony-docker) -->

For PHP8 use the following branch: https://github.com/coloso/symfony-docker/tree/php8-dev  

### Prerequisites
* [Docker](https://www.docker.com/)

### Container
 - [php-fpm](https://hub.docker.com/_/php) 7.4.+
    - [composer](https://getcomposer.org/) 
    - [yarn](https://yarnpkg.com/lang/en/) and [node.js](https://nodejs.org/en/) (if you will use [Encore](https://symfony.com/doc/current/frontend/encore/installation.html) for managing JS and CSS)
 - [nginx](https://hub.docker.com/_/nginx) 1.21.+
 - [mysql](https://hub.docker.com/_/mysql/) 5.7.+

### Installing

run docker and connect to container:
```
 docker compose up --build
```
```
 docker compose exec php sh
```
install the latest version of [Symfony](http://symfony.com/doc/current/setup.html) via composer:
```
# traditional web application: 
composer create-project symfony/website-skeleton .
```
or 
```
# microservice, console application or API:
composer create-project symfony/skeleton .
```

modify your DATABASE_URL config in .env 
```
DATABASE_URL=mysql://root:root@mysql:3306/symfony?serverVersion=5.7
```
### Ready up
call [localhost](http://localhost:81/) in your browser

### Xdebug for VSCode
create .vscode/launch.json with following configuration:
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9005,
            "hostname": "0.0.0.0",
            "pathMappings": {
                "/var/www/symfony": "${workspaceRoot}"
            },
            "log": true,
            "xdebugSettings": {
                "max_children": 100,
                "max_depth": 3
            }
        }
    ]
}
```

### Thanks a lot to
https://github.com/mlocati/docker-php-extension-installer \
https://github.com/denji/nginx-tuning