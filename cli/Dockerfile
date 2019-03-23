FROM php:7.3-cli-alpine

RUN apk --no-cache add postgresql-dev zlib-dev curl-dev icu-dev libzip-dev gmp-dev \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install pgsql pdo_pgsql zip curl mbstring json intl gmp \
    && apk add --no-cache --update --virtual buildDeps $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && apk del buildDeps

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
