FROM php:8.0-fpm-buster
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]
# SHELL: パイプ中あらゆる段階でエラーがあれば失敗とするために pipefail オプションを指定する
# -o: オプションを定義するためのオプション
# -e: そのシェルスクリプト内でエラーが発生したら、以降の処理を中断できる
# -u: 未定義の変数に対して読み込み等を行おうとした際にエラーとなる
# -x: 実行したコマンドを全て標準エラー出力してくれる

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
  apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /work