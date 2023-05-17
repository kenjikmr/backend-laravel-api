# Overview

This is an open source project that implements a news
aggregator website that pulls articles from various sources. It was developed in PHP using the Laravel Framework 10, MySQL database and MVC design pattern. This repository is the Restful API backend only. The frontend is written in ReactJS and can be seen here:

This application a couple of features such as user sign up, user log-in, retrieve user data, personalize news feed preferences and search for Articles in multiple sources like: NewsAPI.org, The Guardian and The New York Times.

## System Requirements (Mac OS, Windows or Linux)
* [Docker](https://www.docker.com/get-started)
* [Docker Compose](https://docs.docker.com/compose/install)
* [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos)

## Project Setup

First clone the repo, run the following commands on bash, inside the root directory:

Copy environment variables of the project: (Notice as this project supports API integration with <b>NewsAPI.org, The Guardian and The New York Times </b>, it means that you MUST set the the api keys for each one of these API's)
```
cp .env.example .env
```

Install project dependencies:
```
composer install
```

Build project artifacts:
```
docker-compose build --no-cache
```

Run project:
```
docker-compose up
```

Install dependencies and set directory permissions and cache:
```
docker exec -it feed-server-php_fpm /bin/sh bootstrap.sh
```

### Notes: 
- Remember to set all the API keys under .env file

After all these steps, the project will be running on port 8080: http://localhost:8080. All http requests send and receive JSON data.


To view changes in the database, go to http://localhost:8181/ on browser and you will be able to access phpmyadmin.

#### OAuth2 User Authentication:

In this API, through Laravel Framework it has been built an OAuth2 related authentication using the library [Passport](https://laravel.com/docs/10.x/passport), then it's possible to consume server side authentication using [JWT](https://jwt.io).

#### Notes:

In **./bootstrap.sh** file are all the commands required to build this project, so, in order to make any changes inside the container, or if you wish to run any other commands, you must run this script and update this file further on if you need to.

- In **all** http requests you must provide the the headers `Accept:application/json`. In POST http requests you need to set the header `Content-Type:application/json`.

- After you hit the sign up or login endpoints, you will be able to get the access_token which will be required on further requests.

- In all http request (except Signup and Login) you need to provide the authentication header: