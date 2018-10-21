FROM php:7.2.11-fpm
LABEL maintrainer="Jakkrapan Wongchan<casanovakung@windowslive.com>"

ARG TZ=Asia/Bangkok

RUN set -x \
  && apt-get update && apt-get install -y \
  zlib1g-dev \
  libicu-dev \
  g++ \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  && docker-php-ext-configure intl \
  && docker-php-ext-install intl \
  && docker-php-ext-configure zip \
  && docker-php-ext-install zip \
  && docker-php-ext-configure mysqli \
  && docker-php-ext-install mysqli \
  && docker-php-ext-configure pdo_mysql \
  && docker-php-ext-install pdo_mysql \
  && cd /tmp \
  && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php \
  && mv /tmp/composer.phar /usr/bin/composer \
  && php -r "unlink('composer-setup.php');" \
  && echo -n

ADD ./zz-overrides.ini /usr/local/etc/php/conf.d/zz-overrides.ini
RUN set -x \
  && mkdir /var/www/.composer \
  && chown -R www-data /var/www/.composer

RUN usermod -u 1000 www-data

EXPOSE 9000
CMD ["php-fpm", "-F"]
