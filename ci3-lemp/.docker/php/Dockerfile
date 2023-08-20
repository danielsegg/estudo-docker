# Use the official PHP image as base
FROM php:7.4-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo_mysql mysqli opcache bcmath exif

# Install xdebug
RUN pecl install xdebug-3.0.4 && docker-php-ext-enable xdebug

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set working directory
WORKDIR /var/www/php

# Define as permissões de escrita na aplicação
RUN find /var/www/php -type d -exec chmod 755 {} \;
RUN find /var/www/php -type f -exec chmod 644 {} \;

# Grupo de permissões
RUN addgroup --gid 1000 gesp
RUN adduser --ingroup gesp --shell /bin/sh gesp
USER gesp

# Expose port 9000 for PHP-FPM
EXPOSE 9000

# Start PHP-FPM
CMD ["php-fpm"]
