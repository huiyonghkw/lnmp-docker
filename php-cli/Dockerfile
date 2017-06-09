# https://github.com/jorge07/alpine-php

FROM alpine:edge

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# https://pkgs.alpinelinux.org/packages

# Mirror mirror switch to Ali-OSM (Alibaba Open Source Mirror Site) - http://mirrors.aliyun.com/
RUN echo 'http://mirrors.aliyun.com/alpine/latest-stable/main' > /etc/apk/repositories \ 
	&& echo '@community http://mirrors.aliyun.com/alpine/latest-stable/community' >> /etc/apk/repositories \ 
	&& echo '@testing http://mirrors.aliyun.com/alpine/edge/testing' >> /etc/apk/repositories

# Mirror mirror switch to Alpine Linux - http://dl-4.alpinelinux.org/alpine/
RUN apk update \
	&& apk upgrade \
	&& apk add \
		curl \
	    php7@community \
	    php7-dev@community \
	    php7-apcu@community \
	    php7-bcmath@community \
	    php7-xmlwriter@community \
	    php7-ctype@community \
	    php7-curl@community \
	    php7-exif@community \
	    php7-iconv@community \
	    php7-intl@community \
	    php7-json@community \
	    php7-mbstring@community\
	    php7-opcache@community \
	    php7-openssl@community \
	    php7-pcntl@community \
	    php7-pdo@community \
	    php7-mysqlnd@community \
	    php7-pdo_mysql@community \
	    php7-pdo_pgsql@community \
	    php7-phar@community \
	    php7-posix@community \
	    php7-session@community \
	    php7-xml@community \
	    php7-simplexml@community \
	    php7-mcrypt@community \
	    php7-xsl@community \
	    php7-zip@community \
	    php7-zlib@community \
	    php7-dom@community \
	    php7-redis@community\
	    php7-tokenizer@community \
	    php7-gd@community \

	 && rm -rf /var/cache/apk/* 

# composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer

CMD ["php", "-a"]
