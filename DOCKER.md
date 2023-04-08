# docker-laradock-example

PHP 개발 환경 예시

## 전체 목차

- [라라독 사용하기](LARADOCK.md)
- [라라벨 사용하기](LARAVEL.md)
- [코드이그나이터 사용하기](CODEIGNITER.md)
- [자주사용하는 도커 명령어](DOCKER.md)

## 자주사용하는 도커 명령어

컨테이너 최초 빌드

```shell
docker-compose up --build
```

컨테이너 빌드 수정 후

```shell
docker-compose up --build --force-recreate
```

컨테이너 시작

```shell
docker-compose up -d
```

컨테이너 제거

```shell
docker-compose down
```

컨테이너 확인

```shell
docker ps -a
```

컨테이너 아이디 확인

```shell
docker ps -aq
```

모든 컨테이너 강제로 제거하기

```shell
docker container rm -f $(docker ps -aq)
```
