FROM php:8.2-apache

# 必要な拡張機能のインストール
RUN docker-php-ext-install pdo pdo_mysql mysqli

# mod_rewriteを有効化（ルーティング用）
RUN a2enmod rewrite

# .htaccessを有効化
RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

WORKDIR /var/www/html