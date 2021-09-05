FROM php:8.0.0-fpm

ARG uid=1000
ARG gid=1000

# Install system dependencies
RUN apt-get update && apt-get install -y apt-utils && apt-get install -y git && apt-get install -y libzip-dev && apt-get install -y zip && apt-get install -y libicu-dev

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql zip intl opcache session

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN groupadd -g $gid dominik \
  && useradd -lm -u $uid -g $gid dominik \
  && chmod +x /usr/bin/composer \
  && chown -R dominik:dominik /var/www

USER dominik

# Set working directory
WORKDIR /var/www