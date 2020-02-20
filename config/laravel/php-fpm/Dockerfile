FROM php:7.4-fpm-alpine

# Instala Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

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

#Extensiones de PHP
RUN set -xe \
    && apk add --update icu \
    && apk add --no-cache --virtual .php-deps make \
    && apk add --no-cache --virtual .build-deps \
        zlib-dev \
        icu-dev \
        g++ \
        imagemagick-dev \
        libtool \
        make \
    && docker-php-ext-install zip mysqli tokenizer opcache pdo pdo_mysql pdo_pgsql mbstring xml bcmath iconv pcntl \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-enable intl \
    && { find /usr/local/lib -type f -print0 | xargs -0r strip --strip-all -p 2>/dev/null || true; } \
    && apk del .build-deps \
    && rm -rf /tmp/* /usr/local/lib/php/doc/* /var/cache/apk/*

RUN apk add --no-cache $PHPIZE_DEPS \
    && pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

RUN pecl install mailparse \
    && docker-php-ext-enable mailparse

RUN apk add --no-cache libpng-dev \
    && docker-php-ext-install gd

RUN apk add --no-cache libmcrypt-dev \
    && yes | pecl install -o -f mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt

# Genera 'locale' para es_AR
RUN cp /usr/share/zoneinfo/America/Argentina/Buenos_Aires /etc/localtime && \
	echo "America/Argentina/Buenos_Aires" > /etc/timezone && \
	apk del tzdata

USER root

RUN echo http://dl-2.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories
RUN apk --no-cache add shadow \
    && usermod -u 1000 www-data

RUN chown -R www-data:www-data /var/www
RUN chown -R www-data:www-data /var/log
RUN chmod 755 /var/www

CMD ["php-fpm"]

WORKDIR /var/www