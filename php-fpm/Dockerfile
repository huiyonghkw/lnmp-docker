#https://store.docker.com/images/9c2c5426-0cca-4a30-a450-b2961541c6dc?tab=description

FROM php:7.1.3-fpm

MAINTAINER bravist <chenghuiyong1987@gmail.com>

RUN apt-get update -y && apt-get install -y zlib1g-dev


# You can install php extensions using docker-php-ext-install

RUN docker-php-ext-install pdo pdo_mysql

RUN docker-php-ext-install zip

RUN docker-php-ext-install gd
