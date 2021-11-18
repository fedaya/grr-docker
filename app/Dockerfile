FROM php:7.3-fpm-bullseye
RUN apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev libxml2-dev m4 re2c autoconf libpng16-16 libjpeg62-turbo libfreetype6 libzip4 build-essential locales locales-all
RUN docker-php-ext-configure gd && \
    docker-php-ext-configure mysqli && \
    docker-php-ext-configure pdo_mysql && \
    docker-php-ext-configure zip && \
    docker-php-ext-configure xml && \
    docker-php-ext-configure mbstring && \
    docker-php-ext-configure opcache
RUN docker-php-ext-install gd mysqli pdo_mysql zip xml mbstring opcache
RUN apt-get purge -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev libxml2-dev m4 re2c autoconf build-essential
RUN apt-get autoremove -y --purge

COPY src /var/www/html
RUN chown -R www-data: /var/www/html/images
RUN chown -R www-data: themes/default/css/types.css


COPY connect.inc.php /var/www/html/include/connect.inc.php
#COPY config.inc.php /var/www/html/include/config.inc.php
#COPY config_ldap.inc.php /var/www/html/include/config_ldap.inc.php
#RUN chown www-data: /var/www/html/include/config_ldap.inc.php

COPY php.ini /usr/local/etc/php/php.ini

COPY docker-php-entrypoint /usr/local/bin/docker-php-entrypoint
RUN chmod +x /usr/local/bin/docker-php-entrypoint

WORKDIR /var/www/html
