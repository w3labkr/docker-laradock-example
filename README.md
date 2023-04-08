# docker-laradock-example

PHP 개발 환경 예시

## 전체 목차

- [라라독 설정하기](LARADOCK.md)
- [라라벨 설정하기](LARAVEL.md)
- [코드이그나이터 설정하기](CODEIGNITER.md)
- [자주사용하는 도커 명령어](DOCKER.md)

## 디렉토리 구조

```txt
.
├── laradock-example/
├── etc-example/
├── laravel-example/
├── codeigniter-example/
└── modern-php/
```

## 라라독 시작하기

STEP 1. 라라독 설치하기

```shell
git clone https://github.com/laradock/laradock.git
```

STEP 2-1. 라라독 설정하기

```shell
cp -a laradock-example/. laradock/
```

STEP 2-2. 호스트 파일 설정하기

```shell
$ vi /c/Windows/System32/drivers/etc/hosts
#
127.0.0.1 localhost
127.0.0.1 laravel.test
127.0.0.1 codeigniter.test
127.0.0.1 modern-php.test
...
::1 localhost
```

STEP 3. 라라독 실행하기

```shell
cd laradock
```

```shell
docker-compose up -d nginx mysql phpmyadmin redis workspace
```

STEP 4. 라라벨 설치하기

```shell
# 컨테이너에 접속하기
$ docker-compose exec --user=laradock workspace bash

# 설치하기
laradock> composer create-project --prefer-dist laravel/laravel laravel -vvv
laradock> exit

# 예제파일 추가하기
$ cp -a laravel-example/. laravel
```

STEP 5. 코드이그나이터 설치하기

```shell
# 컨테이너에 접속하기
$ docker-compose exec --user=laradock workspace bash

# 설치하기
laradock> composer create-project codeigniter4/appstarter codeigniter
laradock> exit

# 예제파일 추가하기
$ cp -a codeigniter-example/. codeigniter
```

STEP 6. 데이터베이스 접속하기

```shell
# 컨테이너에 접속하기
$ docker-compose exec mysql bash

# 데이터베이스 접속하기
root> mysql -uroot -proot
```

STEP 6. phpMyAdmin 접속하기

- URL: http://project.test:8081
- server : mysql
- username : root
- password : root

## 도커 명령어

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

## 참고문헌

- <https://laradock.io/>
