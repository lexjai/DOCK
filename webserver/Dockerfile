
FROM httpd
FROM php:8.1.6-apache
ARG DEBIAN_FRONTEND=noninteractive
RUN docker-php-ext-install mysqli
# Include alternative DB driver
# RUN docker-php-ext-install pdo
# RUN docker-php-ext-install pdo_mysql
RUN apt-get update \
    && apt-get install -y sendmail libpng-dev \
    && apt-get install -y libzip-dev \
    && apt-get install -y zlib1g-dev \
    && apt-get install -y libonig-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install zip

RUN docker-php-ext-install mbstring
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd

RUN a2enmod rewrite

FROM node:14

RUN apt-get update && apt-get install -y apache2

COPY ./src/. /var/www/html

WORKDIR /var/www/html

RUN npm install

RUN a2enmod proxy && a2enmod proxy_http

EXPOSE 80
EXPOSE 3000

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

