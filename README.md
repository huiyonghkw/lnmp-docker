# lnmp-docker
Docker for LNMP (CentOS7 + Nginx + MariaDB + PHP7 + Redis + Supervisor)


## Feature

- Docker Compose
- PHP 7.1
- Nginx (SSL)
- MariaDB
- Redis
- Composer
- HTTPS
- PHP CLI
- PHP FPM 
- Supervisor



## Install docker on CentOS 7

```bash

$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

$ sudo yum makecache fast

$ sudo yum -y install docker-ce

$ sudo systemctl start docker

```
## Install Docker Compose 

open [https://github.com/docker/compose/releases](https://github.com/docker/compose/releases) page. choose the release and download it.

```
$ curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

$ chmod +x /usr/local/bin/docker-compose
```

## Usage

1.clone this repository `lnmp-docker`.

```
$ git clone https://github.com/bravist/lnmp-docker
```


2.go into the `lnmp-docker` directory and build docker images and start up the docker container

```
$ cd lnmp-docker

$ sudo docker-compose build && docker-compose up -d
```




## Mantainance

restart/stop the docker container.

```
$ docker-compose start/stop/restart container_name

```

rebuilt all container. you must locate the `docker-compose.yml` directory.

```
$ docker-compose down

$ docker-compose up -d 
```


enter the docker container.

```
$ docker exec -it lnmp-php-fpm bash
```


install php dependency with composer.

```
$ docker exec -it lnmp-php-fpm bash

$ cd /usr/share/nginx/html/project

$ composer install -vvv
```



## References

- [https://yeasy.gitbooks.io/docker_practice/content/install/centos.html](https://yeasy.gitbooks.io/docker_practice/content/install/centos.html)
