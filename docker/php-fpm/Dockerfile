ARG PHP_VERSION
FROM php:8.0-fpm-alpine

RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
        bash \
        libzip-dev \
        libpng-dev \
    && docker-php-ext-install \
        pdo_mysql \
        bcmath \
        gd \
        opcache \
        zip \
    && apk --update --no-cache add autoconf g++ make
    
# install xdebug
RUN pecl install -f xdebug \
    && docker-php-ext-enable xdebug \
    && apk del --purge autoconf g++ make

# Install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# create working user
ARG USER_ID
ARG GROUP_ID
ARG USER_NAME=app-user

RUN addgroup -g ${GROUP_ID} ${USER_NAME}
RUN adduser -S -u ${USER_ID} -G ${USER_NAME} ${USER_NAME}

# set ownership of composer to user
RUN chown ${USER_NAME}:${USER_NAME} /usr/local/bin/composer

USER ${USER_NAME}

# Setup working directory
WORKDIR /app
