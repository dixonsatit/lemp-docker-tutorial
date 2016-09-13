FROM php:7-fpm-alpine

MAINTAINER Sathit Seethaphon <dixonsatit@gmail.com>

RUN apk upgrade --update && apk --no-cache add \
    git autoconf file g++ gcc binutils isl libatomic libc-dev musl-dev make re2c libstdc++ libgcc libcurl binutils-libs mpc1 mpfr3 gmp libgomp coreutils freetype-dev libjpeg-turbo-dev libltdl libmcrypt-dev libpng-dev openssl-dev libxml2-dev expat-dev icu-dev libmemcached-dev \
    && docker-php-ext-install iconv mysqli pdo pdo_mysql curl bcmath mcrypt mbstring json xml zip bz2 opcache intl  \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && git clone --branch php7 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached \
    && cd /usr/src/php/ext/memcached \
    && docker-php-ext-configure memcached --disable-memcached-sasl \
    && docker-php-ext-install memcached

    # Install Composer && Setup the Composer installer
RUN php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');" \
    && php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('/tmp/composer-setup.php'); } echo PHP_EOL;" \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer  && rm -rf /tmp/composer-setup.php \
    && composer global require --no-progress "fxp/composer-asset-plugin:~1.2.0" 

EXPOSE 9000

CMD ["php-fpm"]
