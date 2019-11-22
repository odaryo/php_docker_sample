ARG PHP_VERSION
FROM php:7.3-fpm-alpine

RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
        bash \
        libpng \
        libpng-dev \
        libjpeg \
        libxml2 \
        libxml2-dev \
    && docker-php-ext-install \
        pdo_mysql \
        mysqli \
        mbstring \
        intl \
        xml \
        opcache \
    && docker-php-ext-enable intl mbstring \
    && apk --update --no-cache add autoconf g++ make
    
# install xdebug
RUN pecl install -f xdebug \
    && docker-php-ext-enable xdebug \
    && apk del --purge autoconf g++ make

# Install composer
RUN curl -sS https://getcomposer.org/installer | php ;mv composer.phar /usr/local/bin/composer;
RUN composer global require hirak/prestissimo

# create users
ARG USER_ID=1000
ARG GROUP_ID=1000

RUN addgroup -g ${GROUP_ID} -S app-user && \
    adduser -u ${USER_ID} -S app-user -G app-user

USER app-user:app-user

# Setup working directory
WORKDIR /app
