FROM php:7-fpm

RUN apt-get update && apt-get upgrade -y \
    g++ \
    libc-client-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libkrb5-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    libpng12-dev \
    libpq-dev \
    libssl-dev \
    libssl-doc \
    libsasl2-dev \
    zlib1g-dev

RUN docker-php-ext-install \
    bz2 \
    iconv \
    mbstring \
    mysqli \
    pgsql \
    pdo_mysql \
    pdo_pgsql \
    soap \
    zip
    
RUN docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    && docker-php-ext-install gd

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN docker-php-ext-install intl
RUN docker-php-ext-install opcache
RUN pecl install mongodb && docker-php-ext-enable mongodb
RUN pecl install redis && docker-php-ext-enable redis
RUN yes '' | pecl install imagick && docker-php-ext-enable imagick
RUN apt-get autoremove -y --purge \
    && apt-get clean \
    && rm -Rf /tmp/*