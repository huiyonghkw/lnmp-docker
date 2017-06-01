#https://store.docker.com/images/9c2c5426-0cca-4a30-a450-b2961541c6dc?tab=description

FROM php:7.1.3-fpm

MAINTAINER bravist <chenghuiyong1987@gmail.com>


# https://hub.docker.com/r/phpdocker/phpdocker/~/dockerfile/

# images
RUN apt-get update \
	&& apt-get install -y \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng12-dev \
	libgd-dev \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install \
		gd \
		exif

# xml
RUN apt-get update \
	&& apt-get install -y \
	libxml2-dev \
	libxslt-dev \
	&& docker-php-ext-install \
		dom \
		xmlrpc \
		xsl

# database
RUN docker-php-ext-install \
	mysqli \
	pdo \
	pdo_mysql

# compression
RUN apt-get update \
	&& apt-get install -y \
	libbz2-dev \
	zlib1g-dev \
	&& docker-php-ext-install \
		zip \
		bz2

# others
RUN docker-php-ext-install \
	mbstring \
	json \
	bcmath

# composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer


WORKDIR /usr/share/nginx/html

# 建立 php-cli 用户，并使用 gosu 换另一个用户执行命令
RUN groupadd -r php-fpm && useradd -r -g php-fpm php

# 下载 gosu
RUN wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.10/gosu-amd64" \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true

CMD ["exec", "gosu", "php-fpm", "php-fpm"]