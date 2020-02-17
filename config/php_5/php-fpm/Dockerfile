FROM php:5.6-fpm-alpine

RUN docker-php-ext-install pdo_mysql

# instalamos paquetes
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

# Genera 'locale' para es_AR
RUN cp /usr/share/zoneinfo/America/Argentina/Buenos_Aires /etc/localtime && \
	echo "America/Argentina/Buenos_Aires" > /etc/timezone && \
	apk del tzdata

CMD ["php-fpm"]

EXPOSE 9000
