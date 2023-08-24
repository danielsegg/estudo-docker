# Use the official PHP image as base
FROM php:7.1-fpm

# Set timezone to America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && echo America/Sao_Paulo > /etc/timezone

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    libicu-dev \
    libonig-dev \
    && rm -r /var/lib/apt/lists/*

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install mbstring, intl, and pdo_mysql extensions
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl mbstring pdo_mysql

# Copy custom PHP configuration
COPY php/php.ini /usr/local/etc/php/conf.d/

# Set the working directory
WORKDIR /var/www/html

# Add write permissions to the 'html' directory
RUN chmod -R 777 /var/www/html

# Expose port 9000 for PHP-FPM
EXPOSE 9000

# Start PHP-FPM
CMD ["php-fpm"]
