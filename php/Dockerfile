FROM php:7.0-fpm

RUN apt-get update && apt-get install -y \
    apt-utils \
    git \
    curl \
    unzip \
    libmcrypt-dev \
    libicu-dev \
    libxml2-dev libxslt1-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    mysql-client \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure hash --with-mhash \
    && docker-php-ext-install -j$(nproc) mcrypt intl xsl gd zip pdo_mysql opcache soap bcmath json iconv

RUN git clone https://github.com/magento/magento2.git /var/www/magento \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/magento

RUN composer install \
    && find var generated vendor pub/static pub/media app/etc -type f -exec chmod u+w {} \; \
    && find var vendor generated pub/static pub/media app/etc -type d -exec chmod u+w {} \; \
    && chmod u+x bin/magento \
    && chown -R www-data:www-data .

CMD php bin/magento setup:install \
    	--db-host=db \
    	--db-name=magento \
    	--db-user=magento \
    	--db-password=123123q \
    	--base-url=http://test.com \
    	--backend-frontname=admin \
    	--admin-user=admin \
    	--admin-password=123123q \
    	--admin-email=admin@test.com \
    	--admin-firstname=Magento \
    	--admin-lastname=User \
    	--language=en_US \
    	--currency=USD \
    	--timezone=America/Chicago \
    	--skip-db-validation \
    && chown -R www-data:www-data . \
    && php-fpm
