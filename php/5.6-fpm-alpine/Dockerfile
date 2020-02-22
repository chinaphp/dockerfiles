FROM php:5.6-fpm-alpine

ARG TZ="Asia/Shanghai"
ENV TZ ${TZ}

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \ 
    && sed -i "s/^;date.timezone =$/date.timezone = \"Asia\/Shanghai\"/" "$PHP_INI_DIR/php.ini-production" \
    && cp "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
    && set -ex \
    && apk upgrade --quiet --no-cache && apk add --no-cache tzdata ca-certificates zlib zlib-dev libmcrypt libmcrypt-dev libltdl \
    && apk add --update --no-cache --virtual .build-deps autoconf build-base \
    && pecl install https://pecl.php.net/get/redis-4.3.0.tgz \
    && docker-php-ext-enable redis \
    && docker-php-ext-install mysqli pdo_mysql mcrypt \   
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && apk add --no-cache libpng libpng-dev freetype freetype-dev libjpeg-turbo libjpeg-turbo-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd && apk del libpng-dev freetype-dev libjpeg-turbo-dev \
    && apk del .build-deps \
    && rm -rf /usr/share/man /tmp/* /var/cache/apk/*