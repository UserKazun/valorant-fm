FROM php:8-fpm

WORKDIR /var/www/html

# PHP実行・デバッグ用、MySQL連携用、作業用で必要なライブラリをインストール
RUN apt-get update \
&& apt-get install -y libonig-dev libzip-dev unzip libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
&& docker-php-ext-install pdo_mysql mbstring zip bcmath \
&& docker-php-ext-configure gd --with-freetype --with-jpeg \
&& docker-php-ext-install -j$(nproc) gd \
&& pecl install xdebug\
&& docker-php-ext-enable xdebug

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 設定ファイルをコピー
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini
COPY ./docker/php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
