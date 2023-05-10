# docker-laradock-example

PHP 개발 환경 예시

## 전체 목차

- [라라독 설정하기](LARADOCK.md)
- [라라벨 설정하기](LARAVEL.md)
- [코드이그나이터 설정하기](CODEIGNITER.md)
- [자주사용하는 도커 명령어](DOCKER.md)

## 라라독 설정하기

라라독 설치하기

```shell
$ git clone https://github.com/laradock/laradock.git
$ cd laradock
```

라라독 환경변수 설정하기

```shell
$ cp .env.example .env
$ vi .env
DB_HOST=mysql
REDIS_HOST=redis
QUEUE_HOST=beanstalkd

### Paths #################################################
APP_CODE_PATH_HOST=../

### PHP Version ###########################################
PHP_VERSION=7.4

### WORKSPACE #############################################
WORKSPACE_INSTALL_WORKSPACE_SSH=true
WORKSPACE_TIMEZONE=Asia/Seoul

### MYSQL #################################################
MYSQL_VERSION=latest

### MARIADB ###############################################
MARIADB_VERSION=latest

### PHP MY ADMIN ##########################################
PMA_DB_ENGINE=mysql
```

## 웹서버 설정하기

윈도우에서 호스트 파일에 도메인 추가하기

```shell
$ vi /c/Windows/System32/drivers/etc/hosts
#
127.0.0.1  localhost
127.0.0.1  project.test
...
::1 localhost
```

리눅스에서 호스트 파일에 도메인 추가하기

```shell
$ vi /etc/hosts
#
127.0.0.1  localhost
127.0.0.1  project.test
...
::1 localhost

$ /etc/init.d/networking restart
```

웹서버에 도메인 추가하기

```shell
$ cp nginx/sites/laravel.conf.example nginx/sites/project.conf
```

```shell
$ vi nginx/sites/project.conf
server {
    ...
    server_name project.test;
    root /var/www/project/public;
    ...
    error_log /var/log/nginx/project_error.log;
    access_log /var/log/nginx/project_access.log;
}
```

URI 확장자 제거하기

```shell
server {
    ...
    location / {
        try_files $uri $uri/ $uri.html $uri.php$is_args$args;
    }
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_param PHP_VALUE "date.timezone=Asia/Seoul;";
    }
    ...
}
```

<https://stackoverflow.com/questions/32100834/how-to-set-php-ini-settings-in-nginx-config-for-just-one-host>

웹서버 설정 파일 적용하기

```shell
docker-compose exec nginx nginx -s reload
```

컨테이너 재구축하기

```shell
docker-compose build nginx
```

컨테이너 재설정하기

```shell
docker-compose up -d --force-recreate nginx
```

컨테이너 재시작하기

```shell
docker-compose restart nginx
```

## PHP-FPM 설정하기

타임존 설정하기

```shell
$ vi .env
...
PHP_FPM_INSTALL_ADDITIONAL_LOCALES=true
PHP_FPM_ADDITIONAL_LOCALES="en_US.UTF-8 es_ES.UTF-8 fr_FR.UTF-8 ko_KR.UTF-8"
PHP_FPM_DEFAULT_LOCALE=ko_KR.UTF-8
```

- <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones>

```shell
$ vi php-fpm/php<PHP_VERSION>.ini
...
date.timezone = Asia/Seoul
short_open_tag = On
display_errors = On
```

컨테이너 재구축하기

```shell
docker-compose build php-fpm
```

컨테이너 재설정하기

```shell
docker-compose up -d --force-recreate php-fpm
```

컨테이너 재시작하기

```shell
docker-compose restart php-fpm
```

## 데이터베이스 설정하기

```shell
$ vi mysql/my.cnf
...
[client]
default-character-set=utf8mb4

[mysql]
default-character-set=utf8mb4

[mysqld]
default-time-zone=Asia/Seoul
character-set-client-handshake=FALSE
character-set-server=utf8mb4
collation-server=utf8mb4_unicode_ci
```

컨테이너 재구축하기

```shell
docker-compose build mysql
```

컨테이너 재설정하기

```shell
docker-compose up -d --force-recreate mysql
```

컨테이너 재시작하기

```shell
docker-compose restart mysql
```

데이터베이스에 접속하기

```shell
# 컨테이너에 접속하기
$ docker-compose exec mysql bash

# 데이터베이스 접속하기
root> mysql -uroot -proot
```
