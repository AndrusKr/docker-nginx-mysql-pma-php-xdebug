FROM php:fpm
ARG TIMEZONE

RUN apt-get update 
RUN apt-get install -y apt-utils

# Install XDebug
RUN pecl install xdebug-2.7.0beta1 \ 
    && docker-php-ext-enable xdebug 

# Docker-php-extentions install/enabled
RUN docker-php-ext-install pdo pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
&& composer --version

# Set Timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
&& printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
&& "date"

# Add configuration files for Php & XDebug
COPY ./php.ini /usr/local/etc/php/php.ini
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

WORKDIR /var/www/code

EXPOSE 80
