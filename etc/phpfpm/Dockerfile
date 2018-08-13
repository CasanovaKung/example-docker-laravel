FROM php:7.2.8-fpm
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
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php \
  && mv /tmp/composer.phar /usr/bin/composer \
  && php -r "unlink('composer-setup.php');" \
  && echo -n

ADD ./zz-overrides.ini /usr/local/etc/php/conf.d/zz-overrides.ini

RUN usermod -u 1000 www-data

EXPOSE 9000
CMD ["php-fpm", "-F"]
