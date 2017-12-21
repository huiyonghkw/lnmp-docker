#https://yeasy.gitbooks.io/docker_practice/content/image/dockerfile/cmd.html
#WebSocket 服务配置
#SOCKET_HTTP_HOST=open.weipeiapp.com.dev
#SOCKET_PORT=8192
#SOCKET_PUBLIC_PORT=8192
#SOCKET_ADDRESS=0.0.0.0
FROM bravist/php-cli-alpine-aliyun-app:1.11

EXPOSE 8192 8193

ENTRYPOINT []

CMD ["/usr/bin/php", "/usr/share/nginx/html/open.weipeiapp.com/artisan", "socket:serve"]
