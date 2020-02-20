FROM php:7.4-fpm-alpine

ARG TZ="Asia/Shanghai"
ENV TZ ${TZ}


RUN set -xe && apk add --quiet --no-cache --virtual=.run-deps tzdata ca-certificates curl tar && \
  # Use the default production configuration
  mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" && \
  docker-php-ext-install pdo_mysql redis gd intl && \
  ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log && \
  ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone && \
    apk del tzdata && \   
	apk del --quiet --no-cache --purge && rm -rf /var/cache/apk/* 
    

# Override with custom opcache settings
#COPY config/opcache.ini $PHP_INI_DIR/conf.d/