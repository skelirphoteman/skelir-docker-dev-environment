FROM php:fpm

RUN apt-get update
RUN apt-get install -y libicu-dev
RUN apt-get install -y libzip-dev


RUN docker-php-ext-install intl
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN docker-php-ext-install zip

RUN docker-php-ext-configure pdo_mysql
RUN docker-php-ext-enable pdo_mysql


ARG INSTALL_ZIP_ARCHIVE=true
RUN if [ ${INSTALL_ZIP_ARCHIVE} = true ]; then \
    # Install the zip extension
    pecl install zip && \
    docker-php-ext-enable zip \
;fi

RUN apt-get update && apt-get -y --no-install-recommends install git \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && rm -rf /var/lib/apt/lists/*
