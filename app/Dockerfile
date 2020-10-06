FROM php:7.3-fpm-alpine

RUN apk add --no-cache build-base freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev libxml2-dev m4 re2c autoconf libpng libjpeg-turbo freetype libzip
RUN docker-php-ext-configure gd && \
    docker-php-ext-configure mysqli && \
    docker-php-ext-configure pdo_mysql && \
    docker-php-ext-configure zip && \
    docker-php-ext-configure xml && \
    docker-php-ext-configure mbstring && \
    docker-php-ext-configure opcache
RUN docker-php-ext-install gd mysqli pdo_mysql zip xml mbstring opcache
RUN apk del build-base freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev libxml2-dev m4 re2c autoconf


COPY src /var/www/html
COPY connect.inc.php /var/www/html/include/connect.inc.php
#COPY config.inc.php /var/www/html/include/config.inc.php
#COPY config_ldap.inc.php /var/www/html/include/config_ldap.inc.php
COPY php.ini /usr/local/etc/php/php.ini
COPY docker-php-entrypoint /usr/local/bin/docker-php-entrypoint

RUN chown -R www-data: /var/www/html/images

WORKDIR /var/www/html