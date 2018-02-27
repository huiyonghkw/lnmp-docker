FROM bravist/php-cli-alpine-aliyun-app:1.12

COPY ./crontabs/default /var/spool/cron/crontabs/

RUN cat /var/spool/cron/crontabs/default >> /var/spool/cron/crontabs/root

WORKDIR /var/spool/cron/crontabs

RUN mkdir -p /var/log/cron \
	&& touch /var/log/cron/cron.log

VOLUME /var/log/cron

CMD ["/usr/sbin/crond", "-f", "-L", "/var/log/cron/cron.log"]
