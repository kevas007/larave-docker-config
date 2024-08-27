# Use the official PHP 8.2 Apache image
FROM php:8.2-apache

# Update package list and install dependencies
RUN apt-get update \
    && apt-get install -y \
        zlib1g-dev \
        g++ \
        git \
        libicu-dev \
        zip \
        libzip-dev \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && a2enmod rewrite

# Set the working directory
WORKDIR /var/www

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Laravel (Laravel's installer via Composer)
RUN composer global require laravel/installer \
    && ln -s ~/.composer/vendor/bin/laravel /usr/local/bin/laravel

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Expose port 80 for the web server
EXPOSE 80
