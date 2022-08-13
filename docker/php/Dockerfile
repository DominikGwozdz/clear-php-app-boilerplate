FROM php:8.1.9-fpm

# 1000 is default primary user on ubuntu
ARG uid=1000
ARG gid=1000

# Install system dependencies
RUN apt-get update &&  \
    apt-get install -y apt-utils &&  \
    apt-get install -y git &&  \
    apt-get install -y libzip-dev &&  \
    apt-get install -y zip &&  \
    apt-get install -y libicu-dev

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql zip intl opcache session

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Use user 1000 as default user in container - fix for non root
RUN groupadd -g $gid $gid \
    && useradd -lm -u $uid -g $gid $uid \
    && chmod +x /usr/bin/composer \
    && chown -R $uid:$gid /var/www

# User 1000 = your user on ubuntu
USER $uid

# Set working directory
WORKDIR /var/www
