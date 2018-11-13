FROM php:5.6.38-fpm-alpine
LABEL maintainer="jinpeng@surveyplus.cn"
ARG version='3.15.3+181108'

# 修改apk源
RUN cp /etc/apk/repositories /etc/apk/repositories.bak
RUN echo "http://mirrors.aliyun.com/alpine/v3.8/main/" > /etc/apk/repositories

# 安装操作系统依赖
RUN apk add --no-cache --virtual .build-deps \
    libpng-dev \
    openldap-dev \
    imap-dev \
    postgresql-dev && \
    apk add --no-cache netcat-openbsd bash tzdata

# 修改时区
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 安装PHP插件
RUN docker-php-ext-configure imap --with-imap-ssl && \
    docker-php-ext-install \
    gd \
    imap \
    ldap \
    mbstring \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    zip

# 下载、解压LimeSurvey包，设置权限
ADD "https://github.com/LimeSurvey/LimeSurvey/archive/${version}.tar.gz" /tmp

RUN tar xzvf "/tmp/${version}.tar.gz" --strip-components=1 -C /var/www/html/ && \
    rm -rf "/tmp/${version}.tar.gz" \
    /var/www/html/docs \
    /var/www/html/tests \
    /var/www/html/*.md && \
    chown -R www-data:root /var/www/ ; \
    chmod -R g=u /var/www

EXPOSE 9000

COPY entrypoint.sh entrypoint.sh
RUN chmod +x entrypoint.sh

ENTRYPOINT ["/var/www/html/entrypoint.sh"]
CMD ["php-fpm"]