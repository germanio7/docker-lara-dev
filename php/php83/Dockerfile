FROM php:8.3-fpm

RUN apt-get update && apt-get install -y \
    libzip-dev zip unzip git curl \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql zip opcache gd

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN composer global require laravel/installer
ENV PATH="$PATH:/root/.composer/vendor/bin"

WORKDIR /var/www/html
