ARG PHPFPM_VERSION

FROM php:${PHPFPM_VERSION}-fpm-alpine

ARG XDEBUG_VERSION
ARG PHPREDIS_VERSION

# Update
RUN apk update && apk upgrade && apk add --no-cache ${PHPIZE_DEPS} procps \
    && pecl install xdebug-${XDEBUG_VERSION} \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache pdo_mysql
# Redis extension
RUN mkdir -p /usr/src/php/ext/redis \
   && curl -L https://github.com/phpredis/phpredis/archive/${PHPREDIS_VERSION}.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
   && echo 'redis' >> /usr/src/php-available-exts \
   && docker-php-ext-install redis
# Cleanup
RUN apk del ${PHPIZE_DEPS} \
    && rm -rf /var/cache/apk/*

#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

WORKDIR /app