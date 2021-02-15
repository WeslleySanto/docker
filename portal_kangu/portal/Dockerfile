FROM ubuntu:18.04

LABEL maintainer 'Weslley Santo <weslley.santo@gmail.com>'

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y locales
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8

# Instalar dependencia de sistema
RUN apt-get update && apt-get install -y \
    apache2 \
    curl \ 
    tzdata \
    ca-certificates \
    iputils-ping \
    software-properties-common 

RUN add-apt-repository -y -u ppa:ondrej/php

#Instalar dependencias PHP 7.1
RUN apt-get update && apt-get install -y php7.1 \
    php7.1-sodium \
    php7.1-apcu \
    php7.1-apcu-bc \
    php7.1-cli \
    php7.1-json \
    php7.1-intl \
    php7.1-simplexml \
    php7.1-opcache \
    php7.1-readline \
    php7.1-xml \
    php7.1-zip \
    php7.1-gd \
    php7.1-mcrypt \
    php7.1-curl \
    php7.1-fileinfo \
    php7.1-ftp \
    php7.1-gettext \
    php7.1-imap \
    php7.1-mbstring \
    php7.1-mysqli \
    php7.1-mysql \
    php7.1-odbc \
    php7.1-soap \
    php7.1-sockets \
    php7.1-xmlrpc \
    php7.1-xsl \
    php7.1-dev \
    php7.1-xdebug \
    # Clear cache
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Configurações apache2
ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

RUN a2enmod rewrite actions asis authz_groupfile cgi headers include vhost_alias

# Instalação e configuração do XDebug
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >>  /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.idekey=docker" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_log=/var/log/xdebug.log" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.default_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini

WORKDIR /var/www/html
CMD ["apachectl", "-D", "FOREGROUND"]

EXPOSE 80