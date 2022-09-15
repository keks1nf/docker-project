FROM php:8.1-fpm

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

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
      yaml \
      ast \
      imagick \
      amqp \
      pcntl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && ln -s $(composer config --global home) /root/composer
ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update -q && apt-get install -qq -y redis-tools sudo
RUN apt-get update -y && apt-get install -y tmux python3 python3-pip supervisor

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    rm -rf /var/lib/apt/lists/*

#RUN apt-get update && apt-get install -y gnupg2
#RUN wget -qO - https://packages.confluent.io/deb/7.0/archive.key | apt-key add -
#RUN add-apt-repository "deb [arch=amd64] https://packages.confluent.io/deb/7.0 stable main"
#RUN add-apt-repository "deb https://packages.confluent.io/clients/deb $(lsb_release -cs) main"
#RUN apt-get update -y && apt-get install -y librdkafka-dev

RUN mkdir -p /home/php/.ssh
RUN ln -s /run/secrets/id_rsa /home/php/.ssh/id_rsa
RUN touch /home/php/.ssh/known_hosts

RUN groupadd -g 1000 php && useradd -u 1000 -g 1000 php && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN chown -R php:php /var/www

RUN curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
RUN sudo apt install -y nodejs

#FROM node:16
#ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

WORKDIR /home/php/

RUN chown -R php:php /home/php /var/www
RUN ln -s /var/www /home/php/www

CMD ["php-fpm"]
