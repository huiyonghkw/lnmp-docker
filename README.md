# lnmp-docker

LNMP Docker Compose (CentOS7 + Nginx + MariaDB + PHP7 + Redis + Supervisor)


## Feature

- Docker Compose
- Nginx (Support ssl certificate)
- MariaDB
- Redis
- PHP 7.0 Cli Container with composer 
- PHP 7.1 FPM Container with composer
- Supervisor
- Guzzle/Curl connections between multiple projects



## Install docker on CentOS 7

> 国内用户，推荐使用[Gitlab-Docker](https://github.com/bravist/gitlab-docker/tree/aliyun)阿里云分支安装Docker 


```bash

$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

$ sudo yum makecache fast

$ sudo yum -y install docker-ce

## start up docker
$ sudo systemctl enable docker

$ sudo systemctl start docker

# Add user to docker group
$ sudo usermod -aG docker $USER

```
## Install Docker Compose

Use the usual commands to install or upgrade Compose. [https://github.com/docker/compose/releases](https://github.com/docker/compose/releases) 
 

```
$ curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

$ chmod +x /usr/local/bin/docker-compose
```

## Usage

1.Clone this repository `lnmp-docker`.

```
$ git clone https://github.com/bravist/lnmp-docker
```

2.Setup the env parameters.

```
$ cp .env.example .env
```


3.Go into the `lnmp-docker` directory and build docker images and start up the docker container

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


## show docker image SIZE using docker images

```bash
$ docker ps 
lnmpdocker_nginx                       latest              8a0bcfaa3d82        26 hours ago        109.4 MB
lnmpdocker_php-supervisor              latest              46b6c174b5bf        26 hours ago        501.2 MB
lnmpdocker_php-fpm                     latest              4f8d95965902        2 days ago          485.9 MB
lnmpdocker_call-websocket              latest              446b4083bbfa        2 days ago          474.1 MB
docker.io/bravist/php-cli-debian-app   1.3                 ceb9aa241524        2 days ago          474.1 MB
docker.io/php                          7.1-fpm             402a94c35023        5 days ago          381.7 MB
docker.io/mariadb                      latest              ea0322bb4096        7 days ago          395.1 MB
docker.io/nginx                        latest              958a7ae9e569        8 days ago          109.4 MB
docker.io/redis                        3.0-alpine          bd87c973dd1a        2 weeks ago         12.64 MB
docker.io/tianon/true                  latest              1298b2036003        11 weeks ago        125 B
```

## show docker metrics using [ctop](https://github.com/bcicen/ctop)

```bash

ctop - 11:02:06 CST      10 containers

   NAME                    CID                     CPU                     MEM                     NET RX/TX               IO R/W                  PIDS

 ◉  gitlabdocker_gitlab_1   9b7e5e64d196                       0%                 2.34G / 7.64G     2.87G / 975M            125M / 844K             0
 ◉  gitlabdocker_postgresq… 20e1381bfb7f                       0%                 133M / 7.64G      4M / 27M                24M / 0B                0
 ◉  gitlabdocker_redis_1    097f239e558d                       0%                  14M / 7.64G      962M / 2.84G            5M / 0B                 0
 ◉  lnmp-call-websocket     a621dd6975ee                       0%                  29M / 7.64G      32K / 3K                816K / 0B               0
 ◉  lnmp-mariadb            c44f11d3a4ef                       0%                 305M / 7.64G      3M / 8M                 132K / 0B               0
 ◉  lnmp-nginx              b0f71da294dd                       0%                  25M / 7.64G      591M / 210M             7M / 0B                 0
 ◉  lnmp-php-fpm            836575e6236d                       0%                  56M / 7.64G      70M / 572M              140K / 0B               0
 ◉  lnmp-php-supervisor     ba5ec6d166a1                       2%                 938M / 7.64G      1.64G / 2.57G           28M / 0B                0
 ◉  lnmp-redis              b8268a9c69c8                       0%                  7M / 7.64G       1.19G / 321M            29K / 408K              0
 ◉  lnmp-www                12830cd7e141                        -                       -           -                       -                       -
 
``` 



## References

- [https://yeasy.gitbooks.io/docker_practice/content/install/centos.html](https://yeasy.gitbooks.io/docker_practice/content/install/centos.html)

- [如何写docker-compose.yml，Docker compose file 参考文档](https://deepzz.com/post/docker-compose-file.html)
