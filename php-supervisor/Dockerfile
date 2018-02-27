FROM bravist/php-cli-alpine-aliyun-app:1.12

MAINTAINER bravist <chenghuiyong1987@gmail.com>

RUN apk update \
	&& apk upgrade \
	&& apk add supervisor \
	&& rm -rf /var/cache/apk/*

# Define mountable directories.
VOLUME ["/etc/supervisor/conf.d", "/var/log/supervisor/"]

# Define working directory.
WORKDIR /etc/supervisor/conf.d

CMD ["supervisord", "--nodaemon", "--configuration", "/etc/supervisor/conf.d/supervisord.conf"]
