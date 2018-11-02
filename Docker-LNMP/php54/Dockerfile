FROM php:5.6-fpm

## Update Ubuntu
RUN apt-get update

## mcrypt
RUN apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mcrypt

## GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev
RUN docker-php-ext-install gd

## Intl
RUN apt-get install -y libicu-dev
RUN docker-php-ext-install intl

## General
RUN docker-php-ext-install zip
RUN docker-php-ext-install pcntl
#RUN docker-php-ext-install opcache
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install mbstring
