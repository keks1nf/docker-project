FROM php:7.4-fpm

ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -qq -y \
      curl \
      git \
      zip unzip \
      wget \
    && install-php-extensions \
      bcmath \
      bz2 \
      calendar \
      exif \
      gd \
      intl \
      ldap \
      memcached \
      mysqli \
      opcache \
      pdo_mysql \
      pdo_pgsql \
      pgsql \
      redis \
      soap \
      xsl \
      zip \
      sockets \
      yaml

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && ln -s $(composer config --global home) /root/composer
ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1

RUN mkdir -p /home/php/.ssh
RUN ln -s /run/secrets/id_rsa /home/php/.ssh/id_rsa
RUN touch /home/php/.ssh/known_hosts

RUN groupadd -g 1000 php && useradd -u 1000 -g 1000 php && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN chown -R php:php /var/www

#ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

WORKDIR /home/php/

RUN chown -R php:php /home/php /var/www
RUN ln -s /var/www /home/php/www

CMD ["php-fpm"]