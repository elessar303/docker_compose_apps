FROM php:7.2-fpm-alpine

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

# instala extensiones de PHP necesarias
RUN docker-php-ext-install mbstring zip mysqli pdo pdo_pgsql pdo_mysql tokenizer xml intl bcmath iconv pcntl

RUN apk add --no-cache libpng-dev \
    && docker-php-ext-install gd

# Genera 'locale' para es_AR (Completar)
RUN cp /usr/share/zoneinfo/America/Argentina/Buenos_Aires /etc/localtime && \
	echo "America/Argentina/Buenos_Aires" > /etc/timezone && \
	apk del tzdata

# agregar usuario para la aplicación laravel
RUN set -x \
    && adduser -D -H -u 1000 -s /bin/bash www-data -G www-data

# copiar los permisos del directorio de la aplicación
RUN chown -R www-data:www-data /var/www
RUN chmod 755 /var/www

# cambiar el usuario actual por www
USER www
WORKDIR /var/www