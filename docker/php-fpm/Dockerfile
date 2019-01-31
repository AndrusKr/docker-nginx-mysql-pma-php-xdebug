FROM php:fpm
ARG TIMEZONE

RUN apt-get update 
RUN apt-get install -y apt-utils
RUN pecl install xdebug-2.7.0beta1 \ 
    && docker-php-ext-enable xdebug 

ADD ./php.ini /usr/local/etc/php/

RUN curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer

WORKDIR /var/www

EXPOSE 80
