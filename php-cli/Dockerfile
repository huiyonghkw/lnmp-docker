#https://store.docker.com/images/9c2c5426-0cca-4a30-a450-b2961541c6dc?tab=description

FROM php:7.1.3-cli

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
RUN docker-php-ext-install mbstring json bcmath

# composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer
COPY composer.json ./
COPY composer.lock ./
RUN composer install --no-scripts --no-autoloader
COPY . ./
RUN composer dump-autoload --optimize && \
	composer run-scripts post-install-cmd

# Run composer and phpunit installation.
RUN composer selfupdate && \
    composer require "phpunit/phpunit:~6.1.4" --prefer-source --no-interaction && \
    ln -s /tmp/vendor/bin/phpunit /usr/local/bin/phpunit

# install supervisord
RUN apt-get install -y supervisor

RUN mkdir -p /var/log/supervisor

WORKDIR /usr/share/nginx/html

COPY ./supervisor/cron.conf /etc/supervisor/conf.d/cron.conf

CMD ["supervisord", "-n"]
