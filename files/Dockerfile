# -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_- -_-
FROM php:7.4.9-fpm-alpine as builder

MAINTAINER Hampster <phper.blue@gmail.com>

# Change source.
RUN echo http://mirrors.aliyun.com/alpine/v3.12/main > /etc/apk/repositories && echo http://mirrors.aliyun.com/alpine/v3.12/community >> /etc/apk/repositories

RUN apk add --no-cache oniguruma-dev && docker-php-ext-install pdo_mysql

WORKDIR /data/code

ADD . .

RUN wget https://mirrors.aliyun.com/composer/composer.phar -O /usr/local/bin/composer \
    && chmod a+x /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer \
    && composer self-update --clean-backups \
    && composer install --no-dev -o \
    && composer dump-autoload -o

RUN chmod +x build.sh

CMD "sh" "build.sh"
