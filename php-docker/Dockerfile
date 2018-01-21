from php:7.0-apache

RUN apt update && apt install -y apt-transport-https git

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/8/prod.list > \
        /etc/apt/sources.list.d/mssql-release.list

RUN apt update && apt install -y \
        freetds-bin \
        freetds-dev \
        freetds-common \
        libct4 \
        libsybdb5 \
        tdsodbc \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libldap2-dev \
        zlib1g-dev \
        libc-client-dev

ENV ACCEPT_EULA Y
RUN apt install -y msodbcsql mssql-tools unixodbc unixodbc-dev

RUN ln -s /usr/lib/x86_64-linux-gnu/libsybdb.so /usr/lib/

RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_dblib
RUN apt install -y libpq-dev
RUN docker-php-ext-install pdo_pgsql

RUN pecl install sqlsrv
RUN echo "extension=sqlsrv.so" >> /usr/local/etc/php/conf.d/sqlsrv.ini
RUN pecl install pdo_sqlsrv
RUN echo "extension=pdo_sqlsrv.so" >> /usr/local/etc/php/conf.d/pdo_sqlsrv.ini

RUN apt install -y locales
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
RUN locale-gen

# RUN docker-php-ext-install pdo_mysql pdo_dblib pdo_odbc --with-pdo-odbc=unixODBC

RUN a2enmod rewrite

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ENV COMPOSER_ALLOW_SUPERUSER 1
