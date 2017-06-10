# https://github.com/jorge07/alpine-php

#FROM bravist/php-cli-alpine-aliyun-app:1.0
FROM php:7.1-fpm-alpine

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# https://pkgs.alpinelinux.org/packages

# Mirror mirror switch to Ali-OSM (Alibaba Open Source Mirror Site) - http://mirrors.aliyun.com/
RUN echo 'http://mirrors.aliyun.com/alpine/latest-stable/main' > /etc/apk/repositories \ 
	&& echo '@community http://mirrors.aliyun.com/alpine/latest-stable/community' >> /etc/apk/repositories \ 
	&& echo '@testing http://mirrors.aliyun.com/alpine/edge/testing' >> /etc/apk/repositories

# Mirror mirror switch to Alpine Linux - http://dl-4.alpinelinux.org/alpine/
#RUN apk update \
#	&& apk upgrade \
#	&& apk add \
#	    php7-fpm@community \

#	 && rm -rf /var/cache/apk/* 

RUN mkdir -p /usr/share/nginx/html

WORKDIR /usr/share/nginx/html

VOLUME /usr/share/nginx/html

#EXPOSE 9000

#ENTRYPOINT ["/usr/sbin/php-fpm7"]

#CMD ["/usr/sbin/php-fpm7", "-R", "--nodaemonize"]


