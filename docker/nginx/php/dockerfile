# Set master image for php
FROM php:8.1-fpm-alpine

# Set working directory
WORKDIR /var/www

RUN apk add oniguruma shadow -q

# Add and Enable PHP-PDO Extenstions
RUN apk add --no-cache zip libzip-dev
RUN docker-php-ext-install pdo pdo_mysql pcntl posix zip
RUN docker-php-ext-enable pdo_mysql pcntl posix

# Install PHP Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Remove Cache
RUN rm -rf /var/cache/apk/*
RUN rm -rf /var/www/html

# Add UID '1000' to www-data
RUN usermod -u 1000 www-data

# Copy existing application directory permissions
COPY --chown=www-data:www-data . /var/www

# Change current user to www
USER www-data

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
