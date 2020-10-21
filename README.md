# Blank Symfony microservice

```
# Build php image
docker build --file ./docker-files/php/Dockerfile --tag soldatov/php:7.4-fpm-bsm .
docker run --rm soldatov/php:7.4-fpm-bsm php -v
docker run --rm soldatov/php:7.4-fpm-bsm php -m

# Build composer image
docker build --file ./docker-files/composer/Dockerfile --tag soldatov/composer:1-bsm .
docker run --rm soldatov/composer:1-bsm php -v
docker run --rm soldatov/composer:1-bsm php -m
docker run --rm soldatov/composer:1-bsm composer --version

# Composer install
docker run --rm --volume .:/app soldatov/composer:1-bsm composer install
# If Windows CMD
docker run --rm --volume %cd%:/app soldatov/composer:1-bsm composer install
# If Windows PowerShell
docker run --rm --volume ${PWD}:/app soldatov/composer:1-bsm composer install
# If Windows Git Bash
docker run --rm --volume /$(pwd):/app soldatov/composer:1-bsm composer install

# if Windows, add in C:\Windows\System32\drivers\etc\hosts: 127.0.0.1 bsm.local
# Domain name in ./docker-files/nginx/default.conf

docker-compose build
docker-compose up -d
```