FROM bravist/php-cli-debian-app:1.2

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# install supervisord
RUN apt-get install -y supervisor \
	&& mkdir -p /var/log/supervisor

COPY ./supervisor/cron.conf /etc/supervisor/conf.d/cron.conf

COPY ./supervisor/log/ /var/log/supervisor/

CMD ["supervisord", "-n"]
