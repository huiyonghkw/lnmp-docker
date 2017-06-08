# https://github.com/jorge07/alpine-php

FROM alpine:edge

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# https://pkgs.alpinelinux.org/packages

RUN echo "@edge-main http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
    && echo "@edge-community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
    && echo "@edge-testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk --no-cache add \
    php7@edge-community \
    php7-dev@edge-community \
    php7-common@edge-community \
    php7-apcu@edge-community \
    php7-bcmath@edge-community \
    php7-xmlwriter@edge-community \
    php7-ctype@edge-community \
    php7-curl@edge-community \
    php7-exif@edge-community \
    php7-iconv@edge-community \
    php7-intl@edge-community \
    php7-json@edge-community \
    php7-mbstring@edge-community \
    php7-opcache@edge-community \
    php7-openssl@edge-community \
    php7-pcntl@edge-community \
    php7-pdo@edge-community \
    php7-mysqlnd@edge-community \
    php7-pdo_mysql@edge-community \
    php7-pdo_pgsql@edge-community \
    php7-phar@edge-community \
    php7-posix@edge-community \
    php7-session@edge-community \
    php7-xml@edge-community \
    php7-simplexml@edge-community \
    php7-mcrypt@edge-community \
    php7-xsl@edge-community \
    php7-zip@edge-community \
    php7-zlib@edge-community \
    php7-dom@edge-community \
    php7-redis@edge-community \
    php7@edge-community \
    php7-tokenizer@edge-community \
    \
    php7-pcntl@edge-community \
    php7-gd@edge-community \
    xmlrpc-c-client@edge-main \
    composer@edge-testing \

    && ln -s /usr/bin/php7 /usr/bin/php

CMD ["php", "-a"]
