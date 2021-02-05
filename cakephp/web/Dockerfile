FROM ubuntu:18.04

LABEL maintainer 'Weslley Santo <weslley.santo@gmail.com>'

RUN apt-get update && apt-get install -y apache2 && apt-get clean

ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

WORKDIR /var/www/html
CMD ["apachectl", "-D", "FOREGROUND"]

EXPOSE 80