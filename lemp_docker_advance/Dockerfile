FROM php:7-fpm-alpine

MAINTAINER Sathit Seethaphon <dixonsatit@gmail.com>

RUN apk add --no-cache \
        freetype \
        libpng \
        libjpeg-turbo \
        freetype-dev \
        libpng-dev \
        libjpeg-turbo-dev \
        icu-dev \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && pecl install intl \
    && docker-php-ext-install -j${NPROC} gd \
    && docker-php-ext-install intl \
    && docker-php-ext-install pdo_mysql \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev
