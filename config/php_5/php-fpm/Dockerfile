FROM php:5.6-fpm-alpine

# Instalamos paquetes para alpine
RUN apk update \
    && apk add \
    wget \
    grep \
    curl \
    tzdata \
    libzip-dev \
    zlib-dev \
    oniguruma-dev \
    zlib \
    icu-dev \
    postgresql-dev \
    libmemcached-dev \
    libxml2-dev \
    git \
    nano

#Paquetes de PHP
RUN docker-php-ext-install mysql pdo_mysql mysqli zip pdo mbstring xml bcmath pgsql pdo_pgsql

RUN apk add --no-cache libpng-dev \
    && docker-php-ext-install gd

# Genera 'locale' para es_AR
RUN cp /usr/share/zoneinfo/America/Argentina/Buenos_Aires /etc/localtime && \
    echo "America/Argentina/Buenos_Aires" > /etc/timezone && \
    apk del tzdata

RUN chown -R www-data:www-data /var/www
RUN chown -R www-data:www-data /var/log

CMD ["php-fpm"]

EXPOSE 9000
