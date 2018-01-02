FROM nginx:1.13.1-alpine

MAINTAINER bravist <chenghuiyong1987@gmail.com>

#https://yeasy.gitbooks.io/docker_practice/content/image/build.html
RUN mkdir -p /etc/nginx/cert \
	&& mkdir -p /etc/nginx/conf.d

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./conf.d/ /etc/nginx/conf.d/
COPY ./cert/ /etc/nginx/cert/

# mount nginx log
VOLUME /var/log/nginx

WORKDIR /usr/share/nginx/html
