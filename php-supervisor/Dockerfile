FROM bravist/php-cli-debian-app:1.3

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# install supervisord
RUN apt-get install -y supervisor \
	&& mkdir -p /var/log/supervisor

COPY ./supervisor/ /etc/supervisor/conf.d/

# Define mountable directories.
VOLUME ["/etc/supervisor/conf.d", "/var/log/supervisor/"]

# Define working directory.
WORKDIR /etc/supervisor/conf.d

ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisor/supervisord.conf"]