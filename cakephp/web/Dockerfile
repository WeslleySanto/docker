FROM ubuntu:18.04

LABEL maintainer 'Weslley Santo <weslley.santo@gmail.com>'

# Instalar dependencia de sistema
RUN apt-get update && apt-get install -y \
    apache2 \
    curl \ 
    software-properties-common 

RUN add-apt-repository ppa:ondrej/php

#Instalar dependencias PHP 5.x
RUN apt-get update && apt-get install -y php5.6 \
    php5.6-ldap \
    php5.6-gd \
    php5.6-mysql \
    php5.6-sybase \
    php5.6-memcached \ 
    php5.6-apcu \
    php5.6-curl \
    php5.6-json \
    php5.6-mcrypt \
    php5.6-readline \
    php5.6-xdebug \
    php5.6-fpm \
    # Clear cache
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

#Instalando composer           
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && mv composer.phar /usr/local/bin/composer

ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

COPY 000-default.conf /etc/apache2/sites-available

WORKDIR /var/www/html
CMD ["apachectl", "-D", "FOREGROUND"]

EXPOSE 80