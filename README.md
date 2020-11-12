# Blank Symfony microservice

Commands
```
docker-compose build --no-cache
docker-compose run --rm bsm-php php -v
docker-compose run --rm bsm-php php -m

# Composer install
docker run --rm --volume .:/app bsm-composer composer install
# If Windows CMD
docker run --rm --volume %cd%:/app bsm-composer composer install
# If Windows PowerShell
docker run --rm --volume ${PWD}:/app bsm-composer composer install
# If Windows Git Bash
docker run --rm --volume /$(pwd):/app bsm-composer composer install

# if Windows, add in C:\Windows\System32\drivers\etc\hosts: 127.0.0.1 bsm.local
# Domain name (bsm.local) indicated in ./docker-files/nginx/default.conf
```

Console commands
```
docker-compose exec phpfpm bin/console doctrine:migrations:status
docker-compose exec phpfpm bin/console doctrine:migrations:generate
```

Setting dev
```
# if Windows, add in C:\Windows\System32\drivers\etc\hosts: 127.0.0.1 servicedesk.local
# File docker-files/dev/nginx/docker-entrypoint.sh must be line separator as LF (\n)
```

Create project
```
cd ..
composer create-project symfony/skeleton app_name
# Copy README.md, docker-files, docker-compose.yml, .gitignore in project 'app_name'.
cd app_name
# Search and replase 'bsm' to 'app_name'.
docker-compose build
docker run --rm --volume %cd%:/app app_name-composer-1:1 composer req api
docker run --rm --volume %cd%:/app app_name-composer-1:1 composer req migrations
docker run --rm --volume %cd%:/app app_name-composer-1:1 composer require symfony/maker-bundle --dev
```