# backend/Dockerfile
FROM php:8.1-fpm

# Установка зависимостей
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    unzip \
    git \
    libpq-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd zip pdo pdo_pgsql

# Копируем файлы проекта
COPY . /var/www

WORKDIR /var/www

# Установка Composer и зависимостей
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN composer clear-cache && composer install

# Установка прав доступа
RUN chown -R www-data:www-data /var/www

EXPOSE 9000
CMD ["php-fpm"]
