# LNMP Docker 

3分钟构建开发、测试、生产L(Alpine Linux ) + N(Nginx) + M(MariaDB) + P(PHP) Docker 容器应用环境。

## 更新日志

### 2017-06-19

+ 新增`php-crond` 周期性任务容器服务，采用`crontab`命令实现，支持宿主机上任意添加定时脚本（PS:`cp default.example default`）

## 主要特性

+ 基于[Alpine Linux](https://alpinelinux.org/) 与 [Debian](https://www.debian.org/index.zh-cn.html) 构建不同基础镜像。master分支基于[Ali-OSM](http://mirrors.aliyun.com/) 加速，在国内环境，5分钟快速完成构建容器集群，alpine 分支基于 [Alpine Linux ](http://dl-4.alpinelinux.org/alpine/)官方镜像，适应非国内环境。debian 分支基于 Docker 官方 debian基础镜像，整体镜像尺寸相对较大。
+ 构建干净、轻量级PHP依赖环境、安装常用PHP扩展与Composer，支持PHP CLI 与 PHP FPM 模式。PHP CLI 适用于命令行交互的项目，PHP FPM 搭配 Nginx，构建PHP Web应用环境。另外，PHP FPM镜像基于 PHP CLI基础镜像，最小化PHP容器镜像，高效利用资源。
+ [Docker Hub 官网](https://hub.docker.com/search/?isAutomated=0&isOfficial=0&page=1&pullCount=0&q=bravist&starCount=0)保留不同Linux版本、不同地域环境的PHP基础镜像。为提高在国内Docker image 构建速度，PHP容器基于阿里巴巴开源镜像服务 -[ALi-OSM Alpine](https://mirrors.aliyun.com/alpine/edge/) 快速完成容器构建。非国内环境，建议克隆[项目 alpine 分支](https://github.com/bravist/lnmp-docker/tree/alpine)实现快速构建，同样也可以尝试debain分支。
+ 提供PHP CLI模式独立运行容器：`call-websockt` 与 `php-superviosr`。`call-websockt`运行基于[workman](http://www.workerman.net/) 的PHP Socket服务。`php-supervior` 实现基于Supervisor的队列服务。
+ 独立配置容器运行时文件、容器运行日志与数据与宿主机分离，方便调试与再次构建容器。
+ 支持Nginx 虚拟站点、SSL证书服务。配置参考Nginx中`cert` 与`conf.d`目录文件。
+ 支持多个虚拟站点之间的程序互通。[参考这里](https://github.com/laradock/laradock/issues/435)了解多个项目间的通信问题。
+ 使用Docker Compose 编排容器，支持在开发、测试、生产环境中快速完成服务器搭建任务。

## 安装LNMP Docker

### 项目依赖

+ CentOS 7
+ Docker 1.12 （Docker要求64位的系统且内核版本至少为3.10）
+ Docker Compose

### 安装Docker 

​	安装Docker 在不同平台、不同地域环境、不同操作系统中的方式不尽相同，这里还是推荐使用[官方CentOS](https://docs.docker.com/engine/installation/linux/centos/)安装方式，其他方法请自行搜索，另外，特别推荐使用阿里云提供的Docker Hub 镜像站点，为你提供专属Docker加速服务。

> [阿里云ECS安装Docker](https://help.aliyun.com/document_detail/51853.html)


```bash
$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

$ sudo yum makecache fast

$ sudo yum -y install docker-ce

# Add docker group
$ sudo groupadd docker

# Add user to docker group
$ sudo usermod -aG docker $USER

## start up docker
$ sudo systemctl enable docker

$ sudo systemctl start docker
```

#### 阿里云Docker Hub镜像站点加速

[阿里云Docker Hub加速器](https://cr.console.aliyun.com/#/accelerator)，需要开通阿里云账户，每一个账户拥有专属加速地址。

```bash
$ sudo mkdir -p /etc/docker
$ sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://muehonsf.mirror.aliyuncs.com"]
}
EOF
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker

```

#### 安装Docker Compose 

推荐Docker  Compose 官方[Gtihub仓库](https://github.com/docker/compose/releases)安装方式，请先选择一个版本。

```bash
$ curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

$ chmod +x /usr/local/bin/docker-compose
```

### 安装LNMP Docker 

1.   克隆项目Git仓库，非国内用户请在克隆后，切换到alpine分支。

     ```bash
     $ git clone https://github.com/bravist/lnmp-docker
     ```

     如果系统未安装git， 可以下载[源码压缩包](https://github.com/bravist/lnmp-docker/releases/tag/1.0)进行安装。

2. 拷贝`.env.example`文件，配置项目环境变量，注意，在容器运行成功后，需要再次修改`.env` 文件，保证多个项目之间的程序互通。

     ```bash
     $ cd lnmp-docker 
     $ cp .env.example .env
     ```

3. 构建容器集群。

     ```bash
     $ docker-compose build && docker-compose up -d
     ```

4. 等待5分钟左右，查看容器是否完成。如果遇到问题，请不要客气的发布你的issue。

     ```bash
     ➜  ~ docker ps
     CONTAINER ID        IMAGE                                   COMMAND                  CREATED             STATUS              PORTS                                                               NAMES
     f4452c868dcc        lnmpdocker_nginx                        "nginx -g 'daemon off"   2 hours ago         Up 2 hours          0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp                            lnmp-nginx
     15182399966b        lnmpdocker_php-supervisor               "supervisord --nodaem"   2 hours ago         Up 2 hours                                                                              lnmp-php-supervisor
     a68c55c28995        bravist/php-fpm-alpine-aliyun-app:1.2   "/usr/sbin/php-fpm7 -"   2 hours ago         Up 2 hours          0.0.0.0:9000->9000/tcp                                              lnmp-php-fpm
     eff86b31f2ba        lnmpdocker_call-websocket               "/usr/bin/php /usr/sh"   2 hours ago         Up 2 hours          0.0.0.0:8190-8191->8190-8191/tcp                                    lnmp-call-websocket
     bd3cecff945e        mariadb                                 "docker-entrypoint.sh"   2 hours ago         Up 2 hours          0.0.0.0:3306->3306/tcp                                              lnmp-mariadb
     279b2f995b2a        lnmpdocker_redis                        "docker-entrypoint.sh"   2 hours ago         Up 2 hours          0.0.0.0:6379->6379/tcp                                              lnmp-redis
     ```

     ​

5. 修改配置文件中的`DOCKER_HOST_IP` 配置参数，这里先要通过`docker inspect` 查询nginx 容器获取。

     ```bash
     $ docker inspect lnmp-nginx | grep IPAddress
                 "SecondaryIPAddresses": null,
                 "IPAddress": "",
                         "IPAddress": "192.168.32.7",
     $ vi .env
     ...
     DOCKER_HOST_IP = 192.168.32.7
     ...
     :wq

     $ docker-compose build && docker-compose up -d
     ```

## 维护

在构建过程中，如果出现问题请第一时间发布issue，这里特别提示：

+ 构建过程中，有两类加速服务，使用阿里云提供的专属镜像加速是为了快速拉取Docker Hub仓库中的远程镜像，而[Ali-OSM](http://mirrors.aliyun.com/) 则是在容器镜像构建软件包的过程中使用它进行快速下载。

+ 全新安装与调试时，尽量将本地Docker 已有容器与镜像清理干净后再尝试。

  ```bash
  # 查看所有运行和者退出的容器
  $ docker ps -a

  # 删除停止的容器
  $ docker rm -f contianer_name ...

  # 快速停止与删除容器集群
  $ docker-compose down 

  # 删除本地docker 镜像
  $ docker rmi -f image_name ....
  ```

+ 进入容器时需要使用`sh` shell登录，因为所有的容器基于Alpine Linux ，默认使用`sh` shell。

  ```bash
  $ docker exec -it lnmp-nginx sh
  ```

### 使用ctop 查询容器占用资源

 [ctop](https://github.com/bcicen/ctop)可以用于查询容器资源占用情况，推荐安装，比如我们的服务器安装了Gitlab与LNMP docker 后的使用情况：

```bash
 $ ctop
 ctop - 15:36:35 CST      10 containers

   NAME                        CID                         CPU                         MEM                         NET RX/TX                   IO R/W                      PIDS

 ◉  gitlabdocker_gitlab_1       97d5ba4b4918                             5%                     1.99G / 7.64G       948M / 1.6G                 120M / 776K                 0
 ◉  gitlabdocker_postgresql_1   146b662e4d62                             0%                      75M / 7.64G        897K / 8M                   24M / 0B                    0
 ◉  gitlabdocker_redis_1        3bcf1582f892                             2%                      14M / 7.64G        1.6G / 940M                 5M / 0B                     0
 ◉  lnmp-call-websocket         eff86b31f2ba                             0%                      66M / 7.64G        3K / 648B                   20M / 0B                    0
 ◉  lnmp-mariadb                bd3cecff945e                             0%                     179M / 7.64G        90K / 276K                  27M / 0B                    0
 ◉  lnmp-nginx                  f4452c868dcc                             0%                      8M / 7.64G         14M / 5M                    5M / 0B                     0
 ◉  lnmp-php-fpm                a68c55c28995                             0%                      72M / 7.64G        1M / 13M                    20M / 0B                    0
 ◉  lnmp-php-supervisor         15182399966b                             1%                     1.8G / 7.64G        92M / 145M                  26M / 0B                    0
 ◉  lnmp-redis                  279b2f995b2a                             0%                      8M / 7.64G         62M / 16M                   2M / 0B                     0
 ◉  lnmp-www                    09c684094c18                              -                           -             -                           -                           -
```

### 查看容器镜像大小

```bash
$ docker images
REPOSITORY                                    TAG                 IMAGE ID            CREATED             SIZE
lnmpdocker_nginx                              latest              8ed67b3d522c        2 hours ago         15.5 MB
lnmpdocker_php-supervisor                     latest              28d1689ec35b        2 hours ago         160.4 MB
lnmpdocker_redis                              latest              61cedd081dd7        2 hours ago         12.63 MB
lnmpdocker_call-websocket                     latest              47883e0cc4cd        2 hours ago         117.9 MB
docker.io/bravist/php-fpm-alpine-aliyun-app   1.2                 1c98507f2de3        2 hours ago         124 MB
docker.io/bravist/php-cli-alpine-aliyun-app   1.0                 505a11124094        24 hours ago        117.9 MB
docker.io/redis                               3.0-alpine          1fbae20f0017        24 hours ago        12.63 MB
docker.io/mariadb                             latest              ea0322bb4096        9 days ago          395.1 MB
docker.io/nginx                               1.13.1-alpine       7ebd6770d0d6        10 days ago         15.49 MB
```

##  参考

> [Docker -- 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/install/centos.html)

  ​