WORKDIR /usr/share/nginx/html

COPY ./supervisor/cron.conf /etc/supervisor/conf.d/cron.conf

COPY ./supervisor/log/ /var/log/supervisor/

CMD ["supervisord", "-n"]
