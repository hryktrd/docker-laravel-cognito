#Cognito検証用サンプルプログラム（Laravel）

## 動作方法

- backend以下に下記の.envファイルを置く。この中にAWSの認証情報が入っている。
  https://drive.google.com/drive/folders/1KDrSdWzhK9J23kEOYtPvftZsRKbhj9i2

- `make up` コマンドでDockerが立ち上がる
  
- `http://localhost` でLaravelの画面が見れる。

- `backend/app/Http/Controllers/Auth/RegisterController.php` ファイル内で`$attributes['custom:role'] = 'producer';`
  いう指定によりカスタム属性を設定している。自己サインアップ後Lambdaが作動し、この属性を読み取って新規登録されたユーザーをプロデューサーグループに移動させる。
  
↓↓↓↓ 以下デフォルトのReadme


# docker-laravel 🐳

![License](https://img.shields.io/github/license/ucan-lab/docker-laravel?color=f05340)
![Stars](https://img.shields.io/github/stars/ucan-lab/docker-laravel?color=f05340)
![Issues](https://img.shields.io/github/issues/ucan-lab/docker-laravel?color=f05340)
![Forks](https://img.shields.io/github/forks/ucan-lab/docker-laravel?color=f05340)

## Introduction

Build a simple laravel development environment with docker-compose.

## Usage

```bash
$ git clone git@github.com:ucan-lab/docker-laravel.git
$ cd docker-laravel
$ make create-project # Install the latest Laravel project
$ make install-recommend-packages # Not required
```

http://localhost

Read this [Makefile](https://github.com/ucan-lab/docker-laravel/blob/master/Makefile).

## Tips

Read this [Wiki](https://github.com/ucan-lab/docker-laravel/wiki).

## Container structure

```bash
├── app
├── web
└── db
```

### app container

- Base image
  - [php](https://hub.docker.com/_/php):8.0-fpm-buster
  - [composer](https://hub.docker.com/_/composer):2.0

### web container

- Base image
  - [nginx](https://hub.docker.com/_/nginx):1.18-alpine
  - [node](https://hub.docker.com/_/node):14.2-alpine

### db container

- Base image
  - [mysql](https://hub.docker.com/_/mysql):8.0

#### Persistent MySQL Storage

By default, the [named volume](https://docs.docker.com/compose/compose-file/#volumes) is mounted, so MySQL data remains even if the container is destroyed.
If you want to delete MySQL data intentionally, execute the following command.

```bash
$ docker-compose down -v && docker-compose up
```
