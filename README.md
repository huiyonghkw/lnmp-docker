# lnmp-docker
Docker for LNMP(CentOS7 + Nginx + MariaDB + PHP7 + Redis)


#### Features (*Recommended for personal use AWS*)

- Amazon Web Service
- CentOS 7
- Docker
- Docker Compose
- PHP 7.0
- Nginx
- MariaDB
- Redis
- PHP Composer
- docker-compose.yml


## Install docker on CentOS 7


CentOS 7 see [Docker Community Edition for CentOS](https://store.docker.com/editions/community/docker-ce-server-centos?tab=description)

Ubuntu see [Docker Community Edition for Ubuntu](https://store.docker.com/editions/community/docker-ce-server-ubuntu?tab=description)

```bash

$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

$ sudo yum makecache fast

$ sudo yum -y install docker-ce

$ sudo systemctl start docker

```


## Install docker compose

see [Install Docker Compose](https://docs.docker.com/compose/install/)


```bash

$ sudo curl -L "https://github.com/docker/compose/releases/download/1.11.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

```


# Usage

1. clone the `lnmp-docker` on CentOS 7


```bash
$ git clone https://github.com/bravist/lnmp-docker
```


2. go to the lnmp-docker and build it with docker-compose

```bash

$ cd lnmp-docker

$ sudo docker-compose build && docker-compose up -d
```



# Mantainance

run the docker

```bash

$ sudo docker-compose start/stop/restart

```

enter the container

``` bash

$ docker exec -it lnmpdocker_nginx_1 /bin/bash
```
