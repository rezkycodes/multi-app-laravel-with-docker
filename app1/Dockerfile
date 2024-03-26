# Gunakan gambar PHP-FPM terbaru
FROM php:8.2.16-fpm-alpine

# Instal ekstensi PHP yang diperlukan
RUN docker-php-ext-install pdo pdo_mysql

# Set direktori kerja
WORKDIR /var/www/html

# Salin kode aplikasi Laravel ke dalam kontainer
COPY . .

# Set izin untuk direktori penyimpanan
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Update app
RUN apk update && apk add --no-cache tzdata
# Set timezone
ENV TZ="Asia/Makassar"

RUN apk add --update --no-cache autoconf g++ make openssl-dev
RUN apk add libpng-dev
RUN apk add libzip-dev
RUN apk add --update linux-headers

RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install sockets
RUN docker-php-ext-install opcache
# COPY docker/php/opcache.ini /usr/local/etc/php/conf.d/opcache.ini
# COPY docker/php/opcache.ini /usr/local/etc/php/conf.d/opcache.ini
# COPY . /var/www/html

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
### End Init install

# Install Redis
# RUN pecl install redis
# RUN docker-php-ext-enable redis

# Install Mongodb
# RUN pecl install mongodb
# RUN docker-php-ext-enable mongodb

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql


#install xdebug
# RUN pecl install xdebug
# COPY 90-xdebug.ini "${PHP_INI_DIR}"/conf.d

# Expose port 9000 dan jalankan PHP-FPM
EXPOSE 9000
CMD ["php-fpm"]