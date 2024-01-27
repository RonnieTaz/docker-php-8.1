FROM php:8.1-cli-alpine3.19

RUN apk --no-cache add curl

COPY --from=composer:2.6 /usr/bin/composer /usr/local/bin/composer

RUN apk --no-cache add zlib-dev \
    $PHPIZE_DEPS \
    libpq-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    openssl-dev \
    libzip-dev \
    unzip \
    zip \
    && pecl install redis \
    && docker-php-ext-configure gd \
    && docker-php-ext-configure zip \
    && docker-php-ext-install \
    gd \
    exif \
    opcache \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    pcntl \
    zip \
    && docker-php-ext-enable redis;

COPY ./docker/php/laravel.ini /usr/local/etc/php/conf.d/laravel.ini

WORKDIR /usr/src/app

ENTRYPOINT ["php", "artisan", "serve"]
