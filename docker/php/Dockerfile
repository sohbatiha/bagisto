FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip
RUN apt-get install -y libzip-dev libicu-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd mysqli zip
RUN docker-php-ext-install intl
RUN pecl install xdebug && docker-php-ext-enable xdebug


#RUN find . -type d -not -perm 755 -exec chmod 755 {} +
#RUN find . -type f -not -perm 644 -exec chmod 644 {} +
#RUN chmod -R g+w storage/logs/
#RUN chmod -R g+w media/files/ media/images/

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php'); "
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

RUN mkdir /var/www/bagisto
# Set working directory
WORKDIR /var/www/bagisto

# USER $user
