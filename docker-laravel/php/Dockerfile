FROM php:7.1-fpm-alpine

RUN mkdir -p /var/www/Projects
WORKDIR /var/www/Projects

RUN sed -i "s/dl-cdn.alpinelinux.org/mirror.tuna.tsinghua.edu.cn/" /etc/apk/repositories

# PHP 环境安装
RUN set -xe \
    && apk add --no-cache \
        freetype-dev \
        libjpeg-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install pdo_mysql gd zip

# 安装 composer
RUN set -xe \
    && php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && rm -f composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.phpcomposer.com

EXPOSE 9000 7001

