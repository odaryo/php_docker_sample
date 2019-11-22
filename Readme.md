# PHP-Dockerコンテナ

## 概要
PHP開発の基本的なものを含めたコンテナです。

## 構成

```
php_docker_sample/
 ├─  app/  　(Laravelのデータ)
 ├─  docker-compose.yml
 └─  docker/   (docker設定ファイル)
      ├─  nginx/
      |    └─  conf.d/
      |         └─  default.conf
      └─  php-fpm/
           ├─  Dockerfile
           └─  conf.d/
                └─  xdebug.ini
```


## 起動方法

### Docker起動

```bash
$ git clone https://github.com/odaryo/php_docker_sample.git .
$ cd php_docker_sample
$ docker-compose build
$ docker-compose up -d
```

### Laravel初期設定
Laravel初期設定

```bash
// コンテナに入る
$ docker-compose exec php-fpm /bin/bash

// 下記はコンテナ内で実行
$ composer install
$ cp .env.example .env
$ php artisan key:generate
$ exit
```

### アクセスURL

localhost:8080

