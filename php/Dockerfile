FROM php:7.3-fpm
ARG GIT_URL
WORKDIR /var/www/magento

RUN apt-get update && apt-get install -y \
    apt-utils \
    git \
    curl \
    unzip libzip-dev \
    libmcrypt-dev \
    libicu-dev \
    libxml2-dev libxslt1-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    mariadb-client
RUN pecl install mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure hash --with-mhash \
    && docker-php-ext-install -j$(nproc) intl xsl gd zip pdo_mysql opcache soap bcmath json iconv sockets \
    && docker-php-ext-enable mcrypt \
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

CMD echo "Running install if needed"; \
    if [ ! -z "${GIT_URL}" ]; then git clone ${GIT_URL} /var/www/magento; fi; \
    if [ ${COMPOSER_INSTALL} = "YES" ]; then sleep 15; composer install \
     && find var generated vendor pub/static pub/media app/etc -type f -exec chmod u+w {} \; \
     && find var vendor generated pub/static pub/media app/etc -type d -exec chmod u+w {} \; \
     && chmod u+x bin/magento \
     && chown -R www-data:www-data . ; \
    fi; \
    if [ ${INSTALL_MAGENTO} = "YES" ]; then sleep 15; \
	php bin/magento setup:install \
    	--db-host=db \
    	--db-name=magento \
    	--db-user=magento \
    	--db-password=123123q \
    	--base-url=http://mage.localhost \
    	--backend-frontname=admin \
    	--admin-user=admin \
    	--admin-password=123123q \
    	--admin-email=admin@localhost.dev \
    	--admin-firstname=Magento \
    	--admin-lastname=User \
    	--language=en_US \
    	--currency=USD \
    	--timezone=America/Chicago \
    	--skip-db-validation ; \
    fi \
    ; chown -R www-data:www-data . \
    ; php-fpm
