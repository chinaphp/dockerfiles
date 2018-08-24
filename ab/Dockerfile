# ab (apache benchmark)
# in a container
#
# docker run --rm -it \
# 	jess/ab
#
FROM alpine:latest
LABEL maintainer "Coffee <chinaphper@qq.com>"

RUN apk --no-cache add \
	apache2-ssl \
	apache2-utils \
	ca-certificates \
	htop

ENTRYPOINT [ "ab" ]