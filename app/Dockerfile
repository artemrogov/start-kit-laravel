FROM php:7.4-fpm

RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd     

RUN curl -sS https://getcomposer.org/installer | php

RUN mv composer.phar /usr/local/bin/composer

RUN chmod +x /usr/local/bin/composer

ARG user
ARG uid

# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u $uid $user

RUN usermod -a -G sudo $user

RUN usermod -a -G www-data $user

WORKDIR /var/www/html/

# Copy existing application directory contents
COPY ./src/ /var/www/html/

# Copy existing application directory permissions
#COPY --chown=www:www ./src/ /var/www/html

# Expose port 9000 and start php-fpm server
EXPOSE 9000

CMD ["php-fpm"]
