FROM php:8.1-fpm

RUN echo 'memory_limit = 2048M' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini 

RUN pecl install xdebug && docker-php-ext-enable xdebug

RUN apt update && apt install unzip git iproute2 libzip-dev libpq-dev zip libxslt1-dev supervisor librabbitmq-dev libssh-dev -y

RUN docker-php-ext-install zip
RUN docker-php-ext-enable zip

RUN docker-php-ext-install pdo bcmath
RUN docker-php-ext-install pdo
RUN pecl install amqp
RUN docker-php-ext-enable amqp

RUN docker-php-ext-install pdo pdo_pgsql
RUN docker-php-ext-enable pdo pdo_pgsql

RUN docker-php-ext-install xsl
RUN docker-php-ext-enable xsl

RUN docker-php-ext-install intl
RUN docker-php-ext-enable intl

RUN pecl install -o -f redis
RUN rm -rf /tmp/pear 
RUN docker-php-ext-enable redis

#configure xdebug
# RUN echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "xdebug.client_port=9003" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "xdebug.client_host=$(ip route show | grep default | grep -o '[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}')" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

#install composer
RUN php -r "copy('https://getcomposer.org/installer','composer-setup.php');"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer

RUN echo 'deb [trusted=yes] https://repo.symfony.com/apt/ /' | tee /etc/apt/sources.list.d/symfony-cli.list
RUN apt update
RUN apt install symfony-cli

RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g yarn