# Blank Symfony microservice

Create docker images env
```
# Build php image
docker build --file ./docker-files/php/Dockerfile --tag bsm-php-7.4:1 .
docker run --rm bsm-php-7.4:1 php -v
docker run --rm bsm-php-7.4:1 php -m

# Build composer image
docker build --file ./docker-files/composer/Dockerfile --tag bsm-composer-1:1 .
docker run --rm bsm-composer-1:1 php -v
docker run --rm bsm-composer-1:1 php -m
docker run --rm bsm-composer-1:1 composer --version

# Composer install
docker run --rm --volume .:/app bsm-composer-1:1 composer install
# If Windows CMD
docker run --rm --volume %cd%:/app bsm-composer-1:1 composer install
# If Windows PowerShell
docker run --rm --volume ${PWD}:/app bsm-composer-1:1 composer install
# If Windows Git Bash
docker run --rm --volume /$(pwd):/app bsm-composer-1:1 composer install

# if Windows, add in C:\Windows\System32\drivers\etc\hosts: 127.0.0.1 bsm.local
# Domain name (bsm.local) indicated in ./docker-files/nginx/default.conf

docker-compose build
docker-compose up -d
docker-compose down
```

Create project
```
cd ..
docker run --rm --volume %cd%:/app bsm-composer-1:1 composer create-project symfony/skeleton app_name
# Copy README.md, docker-files, docker-compose.yml, .gitignore in project 'app_name'.
cd app_name
# Search and replase 'bsm' to 'app_name'.
docker-compose build
docker run --rm --volume %cd%:/app app_name-composer-1:1 composer req api
docker run --rm --volume %cd%:/app app_name-composer-1:1 composer req migrations
docker run --rm --volume %cd%:/app app_name-composer-1:1 composer require symfony/maker-bundle --dev
```

Commands
```
docker-compose exec phpfpm bin/console doctrine:migrations:status
docker-compose exec phpfpm bin/console doctrine:migrations:generate
```