FROM php:7.1-fpm-alpine

COPY php.ini $PHP_INI_DIR/php.ini

# Composer Dependencies
RUN apk --update add \
    bzip2-dev \
    autoconf \
    build-base \
    curl \
    git \
    subversion \
    freetype-dev \
    libjpeg-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libbz2 \
    libstdc++ \
    libxslt-dev \
    openldap-dev \
    make \
    unzip \
    wget && \
    docker-php-ext-install mcrypt zip bz2 mbstring pcntl xsl && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-configure ldap --with-libdir=lib/ && \
    docker-php-ext-install ldap && \
    apk del build-base && \
    rm -rf /var/cache/apk/*



# Register the COMPOSER_HOME environment variable
ENV COMPOSER_HOME /composer

# Add global binary directory to PATH and make sure to re-export it
ENV PATH /composer/vendor/bin:$PATH

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
  && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer \
  && rm -rf /tmp/composer-setup.php

# Set up the working directory
WORKDIR /var/www/app
