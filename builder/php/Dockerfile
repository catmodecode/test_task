FROM php:8.0.6-fpm-alpine3.12

WORKDIR /var/www

RUN apk upgrade --update && apk add --update --no-cache \
    postgresql-dev \
    autoconf \
    git \
    g++ \
    make \
    wget \
    curl \
    freetype \
    libpng \
    libjpeg-turbo \
    freetype-dev \
    libpng-dev \
    libzip-dev \
    libjpeg-turbo-dev &&\
    docker-php-ext-configure gd \
        --with-freetype \
        --with-jpeg && \
    NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    docker-php-ext-install -j${NPROC} gd && \
    apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev \
    libmcrypt-dev

RUN docker-php-ext-install bcmath sockets
RUN docker-php-ext-enable sockets

RUN apk add --update --no-cache libbz2 bzip2-dev

RUN docker-php-ext-install bz2
RUN docker-php-ext-install calendar
RUN docker-php-ext-install exif

RUN apk add --no-cache zip zlib-dev libzip-dev
RUN docker-php-ext-install zip

RUN apk add --no-cache gettext-dev
RUN docker-php-ext-install gettext

RUN apk add --no-cache icu-dev
RUN docker-php-ext-install intl

RUN docker-php-ext-configure intl --enable-intl
RUN docker-php-ext-enable intl
RUN pecl install msgpack
RUN docker-php-ext-enable msgpack
RUN docker-php-ext-install zip
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-enable zip
RUN docker-php-ext-enable msgpack
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install pgsql
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_pgsql

RUN apk add --no-cache libxml2-dev
RUN docker-php-ext-install soap
RUN docker-php-ext-install sysvmsg sysvsem sysvshm

RUN docker-php-ext-install opcache

RUN curl -sS https://getcomposer.org/installer | php -- \
        --filename=composer \
        --install-dir=/usr/local/bin && \
        echo "alias composer='composer'" >> /root/.bashrc

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories;
# ADD localhost.crt /etc/php/localhost.crt

RUN chown -R www-data:www-data ./
USER www-data

CMD ["php-fpm", "--nodaemonize"]
