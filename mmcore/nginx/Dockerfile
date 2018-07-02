FROM php:7.1-fpm

RUN apt-get update \
    && apt-get install -y --no-install-recommends git zip curl \
    && curl --silent --show-error https://getcomposer.org/installer | php && chmod +x composer.phar \
    && ln -s composer.phar /usr/bin/composer \
    && apt-get -y --allow-unauthenticated install libgearman-dev \
    && cd /tmp \
    && git clone https://github.com/wcgallego/pecl-gearman.git \
    && cd pecl-gearman \
    && git checkout gearman-2.0.3 \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && docker-php-ext-enable gearman \
    && apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql