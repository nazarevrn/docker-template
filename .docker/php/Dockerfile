FROM ubuntu:focal


WORKDIR /var/www/html

RUN ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y build-essential software-properties-common \
    nano mc git curl wget
RUN add-apt-repository -y ppa:ondrej/php
RUN apt-get install -y php7.4 composer=1.10.1-1 apache2 php-pear php-dev \
        php7.4-xdebug
#RUN pecl install xdebug-2.5.0 \
#        && docker-php-ext-enable xdebug
#RUN pecl install mcrypt-1.0.2
#RUN docker-php-ext-enable mcrypt

COPY xdebug.ini /etc/php/7.4/mods-available/xdebug.ini
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite
ENV COMPOSER_MEMORY_LIMIT -1
ENV COMPOSER_ALLOW_SUPERUSER 1

RUN usermod -u 1000 www-data && chown -R www-data:www-data /var/www

EXPOSE 80
CMD apachectl -D FOREGROUND