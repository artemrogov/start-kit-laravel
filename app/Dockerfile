FROM ubuntu:18.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update

RUN apt-get install -y software-properties-common

RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get update

RUN apt-get install -y curl git php7.4-cli php7.4-fpm php7.4-intl php7.4-mysql php7.4-mbstring php7.4-zip php7.4-xml php7.4-pgsql 

RUN apt-get install -y \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

ARG user
ARG uid

# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u $uid $user

RUN usermod -a -G sudo $user

RUN usermod -a -G www-data $user

RUN curl -sS https://getcomposer.org/installer | php

RUN mv composer.phar /usr/local/bin/composer

RUN chmod +x /usr/local/bin/composer

EXPOSE 9000

CMD service php7.4-fpm start
