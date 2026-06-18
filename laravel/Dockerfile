FROM composer:2 AS builder

WORKDIR /app
COPY ./app/composer.json ./app/composer.lock ./
RUN composer install --no-dev --no-interaction --prefer-dist --optimize-autoloader

COPY ./app .

FROM php:8.3-fpm-alpine AS runner

RUN docker-php-ext-install pdo pdo_mysql

WORKDIR /var/www/html
COPY --from=builder /app .

EXPOSE 9000
CMD ["php-fpm"]