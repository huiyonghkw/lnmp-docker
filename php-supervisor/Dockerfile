FROM bravist/php-cli-debian-app:1.1

MAINTAINER bravist <chenghuiyong1987@gmail.com>

COPY ./supervisor/cron.conf /etc/supervisor/conf.d/cron.conf

COPY ./supervisor/log/ /var/log/supervisor/

CMD ["supervisord", "-n"]
