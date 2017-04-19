#https://store.docker.com/images/9c2c5426-0cca-4a30-a450-b2961541c6dc?tab=description

FROM php:7.1.3-fpm

MAINTAINER bravist <chenghuiyong1987@gmail.com>

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        zlib1g-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install redis-3.1.2

# You can install php extensions using docker-php-ext-install

RUN docker-php-ext-install pdo pdo_mysql

RUN docker-php-ext-install zip

WORKDIR /usr/share/nginx/html
