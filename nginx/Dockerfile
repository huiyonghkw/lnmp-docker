FROM nginx

MAINTAINER bravist <chenghuiyong1987@gmail.com>

RUN mkdir -R /etc/nginx/cert
RUN mkdir -R /etc/nginx/conf.d 

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./conf.d/ /etc/nginx/conf.d/
COPY ./cert/ /etc/nginx/cert/

