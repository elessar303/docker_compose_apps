FROM php:7.2-fpm

# Instala Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# instala extensiones de PHP necesarias
RUN apt-get update && \
    apt-get install -y libzip-dev zlib1g-dev libonig-dev zlibc libicu-dev libpq-dev libmemcached-dev locales vim.tiny git nano

RUN docker-php-ext-install mbstring zip pdo_pgsql

# Genera 'locale' para es_AR
RUN echo "es_AR.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen
RUN echo "es      es_AR.UTF-8" >> /etc/locale.alias

WORKDIR /var/www