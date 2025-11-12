FROM php:8.2-fpm-alpine

# Обновляем репозитории и устанавливаем зависимости
RUN apk update && apk add --no-cache \
    git \
    curl \
    libpng-dev \
    oniguruma-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev \
    nodejs \
    npm

# Устанавливаем расширения PHP
RUN docker-php-ext-install \
    pdo_mysql \
    mbstring \
    exif \
    pcntl \
    bcmath \
    gd \
    zip

# Устанавливаем Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
# Создаем пользователя для приложения
RUN addgroup -g 1000 app && adduser -u 1000 -G app -s /bin/sh -D app

# Меняем владельца рабочей директории
RUN chown -R app:app /var/www/html

# Переключаемся на пользователя app
USER app

WORKDIR /var/www/html
