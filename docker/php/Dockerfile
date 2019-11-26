FROM php:7.2-fpm

ARG DEBIAN_FRONTEND=noninteractive
ARG ZONE_INFO
ARG LANG
ARG LANG2=${LANG}



RUN apt-get update && apt-get install -y \
        locales locales-all \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        git nano \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-enable zip \
    && docker-php-ext-install -j$(nproc)unzip

ENV LC_ALL=${LANG}
ENV LANGUAGE=${LANG}

RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN ln -snf /usr/share/zoneinfo/${ZONE_INFO} /etc/localtime && echo ${ZONE_INFO} > /etc/timezone

RUN usermod -u 1000 www-data

WORKDIR /var/www/app

#RUN mkdir /run/php
#RUN chown www-data:www-data /run/php
RUN chmod 777 /var/log

RUN chown www-data:www-data /var/www
RUN chown -R www-data:www-data /var/www/app
RUN echo 'memory_limit = 512M' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini;
RUN chown -R www-data:www-data /var/www/app/var/logs
RUN chown -R www-data:www-data /var/www/app/var/cache

EXPOSE 9000
