FROM bravist/nginx:1.0

MAINTAINER bravist <chenghuiyong1987@gmail.com>

# Add logrotate
# https://linux.cn/article-4126-1.html 
# http://xmodulo.com/logrotate-manage-log-files-linux.html 
# http://www.linuxcommand.org/man_pages/logrotate8.html 
# http://linux008.blog.51cto.com/2837805/555829/

RUN apk update \
	&& apk upgrade \
	&& apk add logrotate \
	&& rm -rf /var/cache/apk/* 

COPY ./nginx /etc/logrotate.d/nginx

RUN echo "0       2       *       *       *       /usr/sbin/logrotate -f /etc/logrotate.d/nginx"  >> /var/spool/cron/crontabs/root

CMD ["/usr/sbin/crond"]