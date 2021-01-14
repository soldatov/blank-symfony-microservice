# Blank Symfony microservice
* Nginx 1.19
* PHP 7.4
* Composer 2
* Symfony 5.2
* Postgres 13.1

## Preparation

if Windows, add domain name `bsm.local` in `C:\Windows\System32\drivers\etc\hosts`: `127.0.0.1`.  
Domain name `bsm.local` indicated in `./docker-files/nginx/default.conf`.  
File `docker-files/dev/nginx/docker-entrypoint.sh` must be line separator as LF `\n`.  
Required packages for PHP: [mlocati/docker-php-extension-installer](https://github.com/mlocati/docker-php-extension-installer).  
Add packages in image: `docker-files/dev/php/Dockerfile`. Command `RUN install-php-extensions`.

## Create bsm images (linux)
```
> git clone https://github.com/soldatov/blank-symfony-microservice
> cd blank-symfony-microservice
> cp .env.local.distrib .env.local
> docker-compose build

# Start for test php info. Add bsm.local in hosts file. Open http://bsm.local/
# If Windows, add in C:\Windows\System32\drivers\etc\hosts: 127.0.0.1 bsm.local
> docker-compose up -d
```

## Create project (Linux)
```
> cd app_name
> docker run --rm -v /$(pwd):/app composer create-project symfony/skeleton app_name
> docker run --rm -v /$(pwd):/app composer req symfony/validator
> docker run --rm -v /$(pwd):/app composer req symfony/monolog-bundle
> docker run --rm -v /$(pwd):/app composer req doctrine/annotations
> docker run --rm -v /$(pwd):/app composer req symfony/security-bundle
> docker run --rm -v /$(pwd):/app composer req symfony/maker-bundle --dev

> docker run --rm -v /$(pwd):/app composer req guzzlehttp/guzzle

# Copy docker-files, docker-compose.yml, .env.local.distrib, .gitignore in project 'app_name'.
# Search and replase 'bsm' to 'app_name'.

# If need DB, edit .env param DATABASE_URL
> docker-compose exec composer composer req symfony/orm-pack

> docker run --rm -v /$(pwd):/app composer req nelmio/api-doc-bundle
```

## Create project (Windows)
```
> docker run --rm -v %cd%:/app composer create-project symfony/skeleton app_name
> docker run --rm -v %cd%:/app composer req symfony/validator
> docker run --rm -v %cd%:/app composer req symfony/monolog-bundle
> docker run --rm -v %cd%:/app composer req doctrine/annotations
> docker run --rm -v %cd%:/app composer req symfony/security-bundle
> docker run --rm -v %cd%:/app composer req symfony/maker-bundle --dev

> docker run --rm -v %cd%:/app composer req sguzzlehttp/guzzle

# Copy docker-files, docker-compose.yml, .env.local.distrib, .gitignore in project 'app_name'.
# Search and replase 'bsm' to 'app_name'.

# If need DB, edit .env param DATABASE_URL
> docker-compose exec composer composer req symfony/orm-pack

> docker run --rm -v %cd%:/app composer req nelmio/api-doc-bundle twig asset
```

Useful commands
```
docker-compose build --no-cache
docker-compose run --rm bsm-php php -v
docker-compose run --rm bsm-php php -m

# Composer install
> docker run --rm --volume .:/app bsm-composer composer install
# If Windows CMD
> docker run --rm --volume %cd%:/app bsm-composer composer install
# If Windows PowerShell
> docker run --rm --volume ${PWD}:/app bsm-composer composer install
# If Windows Git Bash (Windows) or Linux
> docker run --rm --volume /$(pwd):/app bsm-composer composer install
```

Symfony console commands
```
> docker-compose exec phpfpm bin/console doctrine:migrations:status
> docker-compose exec phpfpm bin/console doctrine:migrations:migrate
> docker-compose exec phpfpm bin/console doctrine:migrations:generate
```