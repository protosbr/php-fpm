FROM php:5.6-fpm

RUN apt-get update && apt-get upgrade -y \
    g++ \
    libc-client-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libkrb5-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    libpng-dev \
    libpq-dev \
    libssl-dev \
    libssl-doc \
    libsasl2-dev \
    zlib1g-dev

RUN docker-php-ext-install \
    bz2 \
    iconv \
    mbstring \
    mcrypt \
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

RUN curl -o ioncube.tar.gz http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
    && echo "aeed0cfe0c7435338d5c155533bd8f4f176f6f1ccc000465d4c2414ba6bb718a  ioncube.tar.gz"|shasum -c \
    && tar -xvvzf ioncube.tar.gz \
    && mv ioncube/ioncube_loader_lin_5.6.so /usr/local/lib/php/extensions/* \
    && rm -Rf ioncube.tar.gz ioncube \
    && echo "zend_extension=ioncube_loader_lin_5.6.so" > /usr/local/etc/php/conf.d/00_docker-php-ext-ioncube_loader_lin_5.6.ini

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