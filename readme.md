# DEMO SHARING DATABASE BETWEEN TWO LARAVEL APPLICATION THROUGH DOCKER NETWORK 

This repository consist of two laravel application that are sharing the same database connections through docker network.

To demonstrate the flow, we are using default laravel breeze setup, and both application will have same set of users since both are pointing to the same database.

## Installation

Get the first laravel application up and running

```bash
# goto the application directory
cd first-app/
# install php dependencies
composer install
# install npm dependencies
npm install
# spin up the application
docker compose -f docker-compose.yml -f docker-compose.dev.yml up -d
# populate the db with laravel breeze migration structure
docker compose exec app php artisan migrate
```

First laravel app now could be access from http://localhost:8081.
The database could be access through localhost on port 33061.

Get the second laravel application up and running

```bash
# goto the application directory
cd second-app/
# install php dependencies
composer install
# install npm dependencies
npm install
# spin up the application
docker compose -f docker-compose.yml -f docker-compose.dev.yml up -d
```

Second laravel app now could be access from http://localhost:8082.

## Explanation

Since both docker compose are using same docker network name `shared-network`, 
the docker hostnames (`app`, `app2`, `mariadb`) are technically being shared and the 'mariadb' hostname could be access on the second application.

Do notice that in `.env` file of each application the secret for database are same for both and both are referring to `mariadb` hostname.

