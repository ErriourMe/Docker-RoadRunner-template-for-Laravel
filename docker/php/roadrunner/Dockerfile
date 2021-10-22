FROM --platform=linux/amd64 php:8.0-alpine

COPY --from=spiralscout/roadrunner:2.5.0 /usr/bin/rr /usr/bin/rr

RUN addgroup -g 1000 site \
    && adduser -G site -g site -s /bin/sh -D site \
    && mkdir -p /var/run/rr \
    && chown site:site /var/run/rr \
    && chmod -R 777 /var/run/rr

RUN apk update && apk add --no-cache libzip-dev unzip bash

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/
RUN install-php-extensions zip sockets opcache \
    && docker-php-ext-enable opcache