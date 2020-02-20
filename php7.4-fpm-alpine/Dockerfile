FROM php:7.4-fpm-alpine

ARG TZ="Asia/Shanghai"
ENV TZ ${TZ}

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && set -ex \
    && apk update && apk add --no-cache zlib zlib-dev libmcrypt libmcrypt-dev libltdl \
    && apk add --update --no-cache --virtual .build-deps autoconf build-base tzdata \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-install mysqli pdo_mysql \   
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && apk add --no-cache libpng libpng-dev freetype-dev libjpeg-turbo-dev && docker-php-ext-install gd && apk del libpng-dev freetype-dev libjpeg-turbo-dev \
    && apk del .build-deps \
    && rm -rf /usr/share/man /tmp/* /var/cache/apk/*