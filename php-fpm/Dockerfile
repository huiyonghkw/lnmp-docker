# https://github.com/jorge07/alpine-php

FROM bravist/php-cli-alpine-aliyun-app:1.0

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
	    php7-fpm@community \

	 && rm -rf /var/cache/apk/* 

CMD ["php-fpm7"]

EXPOSE 9000
