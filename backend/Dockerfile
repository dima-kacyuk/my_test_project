# backend/Dockerfile
FROM php:8.2-fpm

# Установка зависимостей
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    unzip \
    git \
    libpq-dev \
    nginx \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd zip pdo pdo_pgsql

# Установка Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Копируем файлы проекта
COPY . /var/www

WORKDIR /var/www

# Установка зависимостей через Composer
RUN composer install

# Копируем конфигурацию Nginx
COPY ./docker/nginx/default.conf /etc/nginx/conf.d/default.conf

# Установка прав доступа
RUN chown -R www-data:www-data /var/www

# Открытие порта 80 для Nginx
EXPOSE 80

# Запуск PHP-FPM и Nginx
CMD service nginx start && php-fpm
