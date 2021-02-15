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
    #iputils-ping \
    software-properties-common 

RUN add-apt-repository -y -u ppa:ondrej/php

#Instalar dependencias PHP 7.2
RUN apt-get update && apt-get install -y php7.2 \
    #php7.2-sodium \
    php7.2-apcu \
    php7.2-apcu-bc \
    php7.2-cli \
    php7.2-json \
    php7.2-intl \
    php7.2-simplexml \
    php7.2-opcache \
    php7.2-readline \
    php7.2-xml \
    php7.2-zip \
    php7.2-gd \
    #php7.2-mcrypt \
    php7.2-curl \
    php7.2-fileinfo \
    php7.2-ftp \
    php7.2-gettext \
    php7.2-imap \
    php7.2-mbstring \
    php7.2-mysqli \
    php7.2-mysql \
    php7.2-odbc \
    php7.2-soap \
    php7.2-sockets \
    php7.2-xmlrpc \
    php7.2-xsl \
    php7.2-dev \
    php7.2-xdebug \
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
RUN yes | pecl install xdebug-2.7.2 \
    && echo "zend_extension=$(find /usr/lib/php/ -name xdebug.so)" > /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >>  /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.remote_autostart=on" >> /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.remote_connect_back=on" >> /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.idekey=docker" >> /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.remote_host=host.docker.internal" >> /etc/php/7.2/mods-available/xdebug.ini \
    && echo "xdebug.remote_log=/var/log/xdebug.log" >> /etc/php/7.2/mods-available/xdebug.ini \    
    && echo "xdebug.default_enable=on" >> /etc/php/7.2/mods-available/xdebug.ini


WORKDIR /var/www/html
CMD ["apachectl", "-D", "FOREGROUND"]

EXPOSE 80