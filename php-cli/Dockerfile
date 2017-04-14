#https://store.docker.com/images/9c2c5426-0cca-4a30-a450-b2961541c6dc?tab=description

FROM php:7.1.3-cli

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# You can install php extensions using docker-php-ext-install

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

#Install extensions
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install zip
