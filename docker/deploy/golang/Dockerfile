FROM 1.14.4-alpine3.12 as golang_runtime

FROM alpine3.12

MAINTAINER liiuxuewen@gmail.com

ARG TZ=Asia/Shanghai

COPY --from=golang_runtime /usr/local/go/lib /usr/local/go/lib

RUN \
    apk add --no-cache --virtual .build-tz-deps \
        tzdata \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \

    && apk add --no-cache --virtual .build-ca \
        ca-certificates \

    && apk add --no-cache --virtual .build-ssl \
        libressl \

    && mkdir -p /data/www /data/logs \

    && mkdir -p /data/www /data/logs \

    && echo "hosts: files dns" > /etc/nsswitch.conf

EXPOSE 8080

STOPSIGNAL SIGTERM
