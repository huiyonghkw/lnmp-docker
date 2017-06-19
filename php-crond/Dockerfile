FROM bravist/php-cli-alpine-aliyun-app:1.0

COPY ./crontabs/ /var/spool/cron/crontabs

WORKDIR /var/spool/cron/crontabs

CMD ["/usr/sbin/crond", "-f"]

