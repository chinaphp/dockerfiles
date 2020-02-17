FROM alpine:3.8

ARG TZ="Asia/Shanghai"
ENV TZ ${TZ}
ENV WWW_UID=82 WWW_GID=82

RUN set -xe && (apk --quiet --no-cache upgrade || true) && \
    apk add --quiet --no-cache --virtual=.term-deps rxvt-unicode-terminfo && \
    set -xe && apk add --quiet --no-cache --virtual=.run-deps tzdata nginx git ca-certificates curl tar php5 php5-fpm php5-curl \
    php5-dom php5-intl php5-gd php5-json php5-mcrypt shadow php5-pcntl php5-pdo php5-pdo_pgsql php5-pgsql php5-posix php5-mysqli && \
    curl --location --silent https://github.com/just-containers/s6-overlay/releases/download/v1.22.1.0/s6-overlay-amd64.tar.gz | tar zx -C / && \
    ln -s /usr/bin/php5 /usr/bin/php && adduser -u 82 -D -S -G www-data www-data && \
    ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log && \
    ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone && \
    apk del tzdata && \
    apk del --quiet --no-cache --purge && rm -rf /var/cache/apk/*

COPY resources/ /

# VOLUME /data/web

EXPOSE 80/tcp

RUN set -xe && chmod +x /usr/bin/composer

ENTRYPOINT ["/init"]