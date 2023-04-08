# docker-laradock-example

PHP 개발 환경 예시

## 전체 목차

- [라라독 사용하기](LARADOCK.md)
- [라라벨 사용하기](LARAVEL.md)
- [코드이그나이터 사용하기](CODEIGNITER.md)
- [자주사용하는 도커 명령어](DOCKER.md)

## 디렉토리 구조

```txt
.
├── laradock-example/
│   ├── apache2/
│   ├── mariadb/
│   ├── mysql/
│   ├── nginx/
│   ├── php-fpm/
│   └── .env
├── laravel/
├── codeigniter/
└── modern-php/
```

## 사용하기

컨테이너 실행하기

```shell
docker-compose up -d nginx mysql phpmyadmin redis workspace
```

컨테이너 재구축하기

```shell
docker-compose build nginx mysql phpmyadmin redis workspace
```

컨테이너 재설정하기

```shell
docker-compose up -d --force-recreate nginx mysql phpmyadmin redis workspace
```

컨테이너 캐시 삭제하기

```shell
docker-compose build --no-cache
```

데이터베이스 접속하기

```shell
$ docker-compose exec mysql bash
$ mysql -uroot -proot
```

phpMyAdmin 접속하기

- URL: http://project.test:8081
- server : mysql
- username : root
- password : root

## 참고문헌

- <https://laradock.io/>