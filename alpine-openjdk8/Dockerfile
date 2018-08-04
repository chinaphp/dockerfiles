FROM openjdk:8u171-jdk-alpine3.8

LABEL maintainer="coffee <chinaphper@qq.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}

RUN apk upgrade --update \
    && apk add bash curl tar wget ca-certificates \
        tzdata unzip font-adobe-100dpi ttf-dejavu \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /var/cache/apk/*

CMD ["bash"]