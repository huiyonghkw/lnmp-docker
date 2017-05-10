# lnmp-docker
Docker for LNMP(CentOS7 + Nginx + MariaDB + PHP7 + Redis)


#### Features

- CentOS 7.*
- Docker
- Docker Compose
- PHP 7.1.*
- Nginx
- MariaDB
- Redis
- PHP Composer
- docker-compose.yml
- PHP Dependency: Composer
- HTTPS SSL
- Gitlab
- PostgreSQL


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


## Install docker compose

see [Install Docker Compose](https://docs.docker.com/compose/install/). maybe you visit [github release page](https://github.com/docker/compose/releases) for installing (`Recommend`).


```bash

$ sudo curl -L "https://github.com/docker/compose/releases/download/1.11.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

```

## Gitlab - GitLab is open source software to collaborate on code

As default, you can visit http://ipaddress:8080 when the gitlab image built complete. make sure the host port 80 is open.

### Gitlab backup & restore

visit https://github.com/gitlabhq/gitlabhq/blob/master/doc/raketasks/backup_restore.md

```bash
# This command will create 1494401197_2017_05_10_gitlab_backup.tar on /var/opt/gitlab/backups/
$ sudo gitlab-rake gitlab:backup:create

...
#  Copy the backup file to the server's /mnt/lnmp-docker/gitlab/data/backups
$ sudo cp user@host:/destnation/1494401197_2017_05_10_gitlab_backup.tar user@host:/mnt/lnmp-docker/gitlab/data/backups
...

# This command will overwrite the contents of your GitLab database!
$ sudo gitlab-rake gitlab:backup:restore BACKUP=1494401197_2017_05_10
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


3. how to use composer, more for https://github.com/RobLoach/docker-composer/issues/88#issuecomment-229213544
```bash
$ docker-compose run composer -h
$ docker-compose run composer require dingo/api -vvv
```

in china. your php project maybe to speed up like this

```bash
$ docker-compose run composer config repo.packagist composer https://packagist.phpcomposer.com
```

you can use this command for composer 1.4.1

```bash
$ docker run --rm -ti -v $(pwd):/app lucor/composer -h
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
