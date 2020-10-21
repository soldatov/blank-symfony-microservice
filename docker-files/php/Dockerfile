FROM php:7.4-fpm
RUN apt-get update && apt-get install -y
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/
RUN install-php-extensions pdo_pgsql
WORKDIR /app
