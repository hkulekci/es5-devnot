FROM php:7.1-cli

RUN apt-get update && apt-get install git-core libzip-dev -y \
    && docker-php-ext-install zip

RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer
ADD . /var/www/php-client
WORKDIR /var/www/php-client
RUN composer install

EXPOSE 8080:8080
CMD ["/usr/local/bin/php", "-S", "0.0.0.0:8080", "-t", "public/", "public/index.php"]
#CMD ["composer", "start"]