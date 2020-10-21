FROM composer:1 AS composer
FROM soldatov/php:7.4-fpm-bsm
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN apt-get install -y git libzip-dev unzip \
&& docker-php-ext-install zip \
&& docker-php-ext-enable zip
