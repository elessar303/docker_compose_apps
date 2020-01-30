FROM php:7.2-fpm-alpine

# Instala Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# instala extensiones de PHP necesarias
RUN apk update \
    && apk add libzip-dev zlib-dev oniguruma-dev zlib icu-dev postgresql-dev libmemcached-dev git nano

RUN docker-php-ext-install mbstring zip pdo_pgsql pdo_mysql

# Install language pack
RUN apk --no-cache add ca-certificates wget && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-bin-2.25-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-i18n-2.25-r0.apk && \
    apk add glibc-bin-2.25-r0.apk glibc-i18n-2.25-r0.apk glibc-2.25-r0.apk

# Genera 'locale' para es_AR
COPY ./config/laravel/php-fpm/locale.md /locale.md
RUN cat /locale.md | xargs -i /usr/glibc-compat/bin/localedef -i {} -f UTF-8 {}.UTF-8
ENV LANG=es_AR.UTF-8 \
    LANGUAGE=es_AR.UTF-8

WORKDIR /var/www