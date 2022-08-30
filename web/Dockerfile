FROM php:8.0-apache
RUN apt-get update \
  && apt-get install -y apt-utils zlib1g-dev libpq-dev unzip zip curl cron gettext git nkf libcurl4-openssl-dev libxml2-dev libc-client-dev libkrb5-dev libzip-dev libldap2-dev \
    libpng-dev \
    libmcrypt-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libxml2-dev \
    postgresql-client
RUN apt-get install -y sqlite3 libsqlite3-dev 
RUN apt-get install -y sysv-rc-conf
RUN apt-get install -y vim
RUN apt-get install -y nkf
RUN apt-get install -y locales
RUN sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen
RUN locale-gen
RUN apt-get install -y iproute2
RUN apt-get install -y iputils-ping
RUN apt-get install -y wget

# PHP8.0向けgdインストール方法
RUN docker-php-ext-configure gd --with-jpeg && docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install curl 
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl && docker-php-ext-install -j$(nproc) imap
RUN docker-php-ext-install intl 
RUN docker-php-ext-install simplexml xml xmlwriter
RUN docker-php-ext-install ldap
RUN docker-php-ext-install ctype
RUN docker-php-ext-install exif 
# RUN docker-php-ext-install fileinfo 
# RUN docker-php-ext-install wddx 
RUN docker-php-ext-install gettext
RUN docker-php-ext-install mbstring 
RUN docker-php-ext-install pdo pgsql pdo_pgsql 
RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install sockets
# RUN docker-php-ext-install phar 
RUN docker-php-ext-install zip
# RUN docker-php-ext-install json
RUN apt-get -y clean

# #下記はproduction環境では利用しないこと
# RUN pecl install xdebug-2.7.0beta1
# RUN docker-php-ext-enable xdebug

# composerのインストールはcomposerイメージから取ってきたほうが楽みたい
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer 

# その他apache設定
RUN a2enmod cgid
WORKDIR /var/www
RUN chown -R www-data:www-data html

# mod_rewriteを 有効に
RUN a2enmod rewrite
