# Use the official PHP image with Apache
FROM php:8.2-apache

# Install dependencies, Tesseract OCR, enable GD, enable mod_rewrite, and clean up
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    tesseract-ocr \
    && docker-php-ext-install gd \
    && a2enmod rewrite \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

    # Install required PHP extensions
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Copy composer if not already present
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

    # Install Composer dependencies
RUN composer install --no-dev --optimize-autoloader

# Copy source code into Apache server directory
COPY . /var/www/html/

# Set permissions
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html
