FROM php:7.4.3-fpm-alpine3.11

ARG TZ="Asia/Shanghai"
ENV TZ ${TZ}

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && cp "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
    && sed -i "s/^;date.timezone =$/date.timezone = \"Asia\/Shanghai\"/" /usr/local/etc/php/php.ini \
    && set -ex \
    && apk update && apk add --no-cache tzdata zlib zlib-dev libmcrypt libmcrypt-dev libltdl \
    && apk add --update --no-cache --virtual .build-deps autoconf build-base \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-enable opcache \
    && docker-php-ext-install mysqli pdo_mysql \   
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && apk add --no-cache libpng libpng-dev freetype freetype-dev libjpeg-turbo libjpeg-turbo-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd && apk del libpng-dev freetype-dev libjpeg-turbo-dev \
    && apk del .build-deps \
    && rm -rf /usr/share/man /tmp/* /var/cache/apk/*