# https://github.com/jorge07/alpine-php

FROM alpine:edge

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# https://pkgs.alpinelinux.org/packages

# Mirror mirror switch to Ali-OSM (Alibaba Open Source Mirror Site) - http://mirrors.aliyun.com/
RUN echo 'http://mirrors.aliyun.com/alpine/latest-stable/main' >> /etc/apk/repositories \
	&& echo 'http://mirrors.aliyun.com/alpine/latest-stable/community' >> /etc/apk/repositories

# Mirror mirror switch to Alpine Linux - http://dl-4.alpinelinux.org/alpine/
RUN apk update \
	&& apk upgrade \
	&& apk add \
		curl \
	    php7 \
	    php7-dev \
	    php7-apcu \
	    php7-bcmath \
	    php7-xmlwriter \
	    php7-ctype \
	    php7-curl \
	    php7-exif \
	    php7-iconv \
	    php7-intl \
	    php7-json \
	    php7-mbstring \
	    php7-opcache \
	    php7-openssl \
	    php7-pcntl \
	    php7-pdo \
	    php7-mysqlnd \
	    php7-pdo_mysql \
	    php7-pdo_pgsql \
	    php7-phar \
	    php7-posix \
	    php7-session \
	    php7-xml \
	    php7-simplexml \
	    php7-mcrypt \
	    php7-xsl \
	    php7-zip \
	    php7-zlib \
	    php7-dom \
	    php7-redis \
	    php7-tokenizer \
	    php7-gd \

	 && rm -rf /var/cache/apk/* 

# composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer

CMD ["php", "-a"]
