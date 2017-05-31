# lnmp-docker
Docker for LNMP(CentOS7 + Nginx + MariaDB + PHP7 + Redis)


#### Features

- CentOS 7.*
- Docker Compose
- PHP 7.1.*
- Nginx
- MariaDB
- Redis
- Composer
- HTTPS


## Install docker on CentOS 7

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

more see [Docker Community Edition for CentOS](https://store.docker.com/editions/community/docker-ce-server-centos?tab=description)


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
