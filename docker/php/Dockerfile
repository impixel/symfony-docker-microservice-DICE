FROM php:7.2-fpm

LABEL licence = "MIT"
LABEL maintainer = "Hadi Tajallaei"

RUN apt-get update -y && apt-get install -y \
    apt-utils \
    git \
    unzip \
    libsasl2-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libicu-dev \
    libxrender1 \
    libzip-dev \
    libxml2-dev \
    libfontconfig1 \
    gcc-6-base \
    libc6 \
    libgcc1 \
    libsodium18 \
    libsodium-dev \
    libbz2-dev \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install opcache \
    && docker-php-ext-install intl \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install sodium

RUN pecl update-channels \
    && pecl install mongodb-1.4.2 \
    && echo "extension=mongodb.so" >> /usr/local/etc/php/conf.d/docker-php-ext-mongodb.ini \
    && pecl install apcu-5.1.11 \
    && echo "extension=apcu.so" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini \
    && pecl install xdebug-2.7.0alpha1

COPY php/config/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

COPY php/config/php.ini /usr/local/etc/php/

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version

RUN chown -R www-data:www-data /var/www

WORKDIR /var/www