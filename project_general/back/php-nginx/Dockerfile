FROM php:7.4-fpm

RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip nginx \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
#RUN git config --global user.email "you@example.com" \ 
#    && git config --global user.name "Your Name"

COPY ./php-artifacts /var/www/symfony_docker
COPY ./entrypoint.sh /etc/entrypoint.sh

RUN chown -R www-data:www-data /var/www /var/log /var/lib/nginx /var/run /run
USER www-data

WORKDIR /var/www/symfony_docker
RUN composer install \
    --no-interaction \
    --no-plugins \
    --no-scripts \
    --optimize-autoloader \
    --prefer-dist && \
    rm -rf /home/www-data/.composer/cache

ENTRYPOINT ["/etc/entrypoint.sh"]
