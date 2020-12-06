# RUNTIME
FROM php:8.0-apache

RUN apt-get update -y \
&& apt-get install -y libpq-dev vim git zip unzip \
&& docker-php-ext-install pdo pdo_pgsql pdo_mysql sockets bcmath opcache \
&& docker-php-ext-configure pgsql --with-pgsql \
&& docker-php-ext-configure bcmath --enable-bcmath \
&& pecl install xdebug apcu \
&& docker-php-ext-enable apcu xdebug

WORKDIR /var/www

COPY ./php.ini /usr/local/etc/php/
COPY ./000-default.conf /etc/apache2/sites-available

RUN a2enmod rewrite

# COMPOSER
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# NODE
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - \
&& apt-get install -y nodejs build-essential \
&& npm i -g newman newman-reporter-html
