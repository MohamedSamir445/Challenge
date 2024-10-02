FROM php:8.2-fpm-alpine

# Install system dependencies
RUN apk add --no-cache \
    libpng-dev \
    libjpeg-turbo-dev \
    libwebp-dev \
    libxpm-dev \
    libzip-dev \
    unzip \
    git \
    bash \
    curl \
    libxml2-dev \
    oniguruma-dev \
    postgresql-dev \
    libmcrypt-dev

# Install PHP extensions
RUN docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-webp=/usr/include/ --with-xpm=/usr/include/
RUN docker-php-ext-install gd zip pdo pdo_mysql pdo_pgsql mbstring xml

# Set the working directory
WORKDIR /var/www

# Copy the existing application directory contents
COPY . .

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install PHP dependencies
RUN composer install --no-interaction --prefer-dist

# Expose the port the app runs on
EXPOSE 9000

# Start the PHP FastCGI Process Manager
CMD ["php-fpm"]
