# Slim Framework 3 Skeleton Application running on Docker Compose

This is a sample PHP app ([Slim 3 Skeleton](https://github.com/slimphp/Slim-Skeleton)) running on [Docker Compose](https://docs.docker.com/compose/).

## Install the Application

Run these commands in the directory where you download the code.

1. Start the docker-compose services (PHP, Nginx) in the background (detached):
  ```
$ docker-compose up -d
  ```

2. Run the Composer installer in the PHP container to install the PHP dependencies:
  ```
$ docker-compose exec php composer install
  ```

The application should now be available on [http://localhost:8080](http://localhost:8080).
