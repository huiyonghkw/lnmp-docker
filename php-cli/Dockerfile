#https://store.docker.com/images/9c2c5426-0cca-4a30-a450-b2961541c6dc?tab=description

FROM php:7.1.3-cli

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# https://hub.docker.com/r/phpdocker/phpdocker/~/dockerfile/

# images
RUN apt-get update \
	&& apt-get install -y \
	apt-utils \
	wget \
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

# https://yeasy.gitbooks.io/docker_practice/content/image/build.html
RUN docker-php-ext-install \
	mbstring \
	json \
	bcmath

# composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer

# install supervisord
RUN apt-get install -y supervisor \
	&& mkdir -p /var/log/supervisor

# https://yeasy.gitbooks.io/docker_practice/content/image/dockerfile/user.html
# 建立 php-cli 用户，并使用 gosu 换另一个用户执行命令
RUN groupadd -r php-cli && useradd -r -g php-cli php

# 下载 gosu
RUN wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.10/gosu-amd64" \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true


WORKDIR /usr/share/nginx/html

COPY ./supervisor/cron.conf /etc/supervisor/conf.d/cron.conf

# 设置 CMD，并以另外的用户执行
# CMD ["supervisord", "-n"]
CMD [ "exec", "gosu", "php-cli", "supervisord", "-n" ]
