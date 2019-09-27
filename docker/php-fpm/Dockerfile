FROM php:7.1-fpm-alpine

ENV MONGO_PHP_DRIVER_VERSION=1.3.4

RUN docker-php-source extract && \
  apk add --update --no-cache \
            autoconf \
            file \
            libc-dev \
            make \
            zlib-dev \
            libpng \
            libpng-dev \
            libxml2-dev \
            libmcrypt-dev \
            pkgconf \
            re2c \
            pcre-dev \
            openssl-dev \
            icu-dev \
            g++ \
            git && \
  docker-php-ext-install mysqli && \
  docker-php-ext-install pdo && \
  docker-php-ext-install pdo_mysql && \
  docker-php-ext-install mbstring && \
  docker-php-ext-install tokenizer && \
  docker-php-ext-install gd && \
  docker-php-ext-install zip && \
  docker-php-ext-install xml && \
  docker-php-ext-install dom && \
  docker-php-ext-install mcrypt && \
  docker-php-ext-install json && \
  docker-php-ext-install intl && \
  docker-php-ext-install iconv && \
  docker-php-ext-install bcmath && \
  echo "Install composer..." && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer  && \
  echo "Install MongoDB extension for PHP 7 ..." && \
    git clone --depth=1 -b ${MONGO_PHP_DRIVER_VERSION} https://github.com/mongodb/mongo-php-driver.git /tmp/php-mongodb && \
        cd /tmp/php-mongodb && \
        git submodule update --init && \
        phpize && ./configure --prefix=/usr && make && make install && \
        cd .. && rm -rf /tmp/php-mongodb/ && \
        echo 'extension=mongodb.so' >> /usr/local/etc/php/conf.d/mongodb.ini && \
  echo "Cleaning sources and files not used ..." && \
    docker-php-source delete  && \
    rm -rf /var/cache/apk/*  && \
    rm -rf /tmp/*



WORKDIR "/rt"

EXPOSE 9000