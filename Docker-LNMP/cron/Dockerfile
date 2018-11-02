FROM php:7.1-cli

COPY ../files/sources.list.jessie /etc/apt/sources.list

## Update Ubuntu
RUN apt-get update

## mcrypt
RUN apt-get install -y libmcrypt-dev
RUN docker-php-ext-configure mcrypt
RUN docker-php-ext-install -j$(nproc) iconv mcrypt

## GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

## Intl
RUN apt-get install -y libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

## General
RUN docker-php-ext-install zip
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install opcache
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli

# Required by cron
RUN apt-get install -y cron vim

RUN ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

#job file
ADD crontab /etc/cron.d/cron

RUN mkdir /var/log/cron
RUN touch /var/log/cron/cron.log

RUN chmod 0644 /etc/cron.d/cron

RUN crontab /etc/cron.d/cron

CMD ["cron", "-f"]
