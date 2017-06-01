#https://yeasy.gitbooks.io/docker_practice/content/image/dockerfile/cmd.html
FROM bravist/php-cli-debian-app:1.2

EXPOSE 8190 8191

COPY ./start.php /usr/share/nginx/html/start.php

ENTRYPOINT ['/usr/local/bin/php' ,'start', '/usr/share/nginx/html/start.php']