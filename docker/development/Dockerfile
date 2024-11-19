FROM php:8.2-fpm

ENV COMPOSER_HOME /tmp

RUN apt-get update

RUN apt-get install -y \
    git \
    libicu-dev \
    libpq-dev \
    libzip-dev \
    locales \
    unzip

RUN pecl install xdebug

RUN docker-php-ext-configure intl

RUN docker-php-ext-install -j$(nproc) intl pcntl pdo pdo_pgsql zip

RUN docker-php-ext-enable xdebug && \
    echo "xdebug.mode=coverage" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini;

COPY --from=composer/composer /usr/bin/composer /usr/bin/composer
