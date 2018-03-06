# PHP-FPM Docker Image
Docker container to install and run [PHP-FPM](https://php-fpm.org/).

[![Build Status](https://travis-ci.org/protosprojetos/php-fpm.svg?branch=master)](https://travis-ci.org/protosprojetos/php-fpm) [![Automated Build](https://img.shields.io/docker/automated/jrottenberg/ffmpeg.svg)](https://hub.docker.com/r/protosprojetos/php-fpm/builds/)

## Supported branches and respective Dockerfile links

**Note:** The master branch will always have the latest version of PHP

 - 7.2 [Dockerfile](https://github.com/protosprojetos/php-fpm/blob/master/Dockerfile)
 - 7.1 [Dockerfile](https://github.com/protosprojetos/php-fpm/blob/7.1/Dockerfile)
 - 5.6 [Dockerfile](https://github.com/protosprojetos/php-fpm/blob/5.6/Dockerfile)

## What is PHP-FPM ?
PHP-FPM (FastCGI Process Manager) is an alternative FastCGI implementation for PHP.

## Getting image
```sh
sudo docker pull protosprojetos/php-fpm
```

## Running your PHP script

### Running image
Run the PHP-FPM image, mounting a directory from your host.

```sh
sudo docker run -it --name phpfpm -v /path/to/your/app:/var/www/html protosprojetos/php-fpm php index.php
```

or using [Docker Compose](https://docs.docker.com/compose/):

```sh
version: '3'
services:
  phpfpm:
    container_name: phpfpm
    image: protosprojetos/php-fpm
    entrypoint: php index.php
    volumes:
      - /path/to/your/app:/var/www/html
```

### Running as server

```sh
sudo docker run --rm --name phpfpm -v /path/to/your/app:/var/www/html -p 8181:8181 protosprojetos/php-fpm php-fpm -S="0.0.0.0:8181" -t="/var/www/html"
```

### Logging
```sh
sudo docker logs phpfpm
```

# Listing installed extensions

```sh
sudo docker run --rm -it protosprojetos/php-fpm php -m
```

# Credits
https://github.com/nanoninja/php-fpm