FROM composer:1 AS composer
FROM bsm-php-7.4:1
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN install-php-extensions zip
