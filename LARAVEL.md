# docker-laradock-example

PHP 개발 환경 예시

## 전체 목차

- [라라독 설정하기](LARADOCK.md)
- [라라벨 설정하기](LARAVEL.md)
- [코드이그나이터 설정하기](CODEIGNITER.md)
- [자주사용하는 도커 명령어](DOCKER.md)

## 라라벨 설정하기

```shell
$ docker-compose exec --user=laradock workspace bash
$ cd /var/www/project
```

설치하기

```shell
composer create-project --prefer-dist laravel/laravel . -vvv
```

키 생성하기

```shell
php artisan key:generate
```

업데이트하기

```shell
composer update
```

배포하기

```shell
composer install --no-dev
```

캐시 삭제하기

```shell
php artisan cache:clear && php artisan view:clear && php artisan config:cache
```
