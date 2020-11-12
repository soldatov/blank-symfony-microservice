FROM composer:1 AS composer
FROM bsm-php
RUN install-php-extensions zip
COPY --from=composer /usr/bin/composer /usr/bin/composer
