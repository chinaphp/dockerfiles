FROM combro2k/alpine-base:latest

ARG TZ="Asia/Shanghai"
ENV TZ ${TZ}
ENV WWW_UID=82 WWW_GID=82

RUN set -xe && apk add --quiet --no-cache --virtual=.run-deps tzdata nginx git ca-certificates curl tar php7 php7-fpm php7-curl php7-dom php7-gd php7-iconv php7-xml \
  php7-json php7-mcrypt php7-pcntl php7-intl php7-mbstring php7-redis php7-pdo php7-pdo_pgsql php7-pgsql php7-posix php7-mysqli php7-session php7-ctype && adduser -u 82 -D -S -G www-data www-data && \
  ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log && \
  ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone && \
    apk del tzdata && \
	apk del --quiet --no-cache --purge && rm -rf /var/cache/apk/*

COPY resources/ /

#VOLUME /data/web

EXPOSE 80/tcp

RUN set -xe && chmod +x /usr/bin/composer