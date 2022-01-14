FROM php:8.0-fpm AS prod

ARG WWWUSER=1100
ARG WWWGROUP=1100

ENV PATH="/var/www/.composer/vendor/bin:${PATH}"

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin

RUN apt-get update && apt install -y \
    git \
    ffmpeg \
    jq \
    iputils-ping


RUN chmod +x /usr/local/bin/install-php-extensions && sync \
    && install-php-extensions \
    gd \
    bcmath \
    opcache \
    xsl \
    imap \
    zip \
    ssh2 \
    yaml \
    pcntl \
    intl \
    sockets \
    ldap \
    oci8 \
    pdo_mysql \
    @composer

RUN usermod -u "$WWWUSER" www-data \
    && groupmod -g "$WWWGROUP" www-data


WORKDIR /var/www/html

################################
#          dev stage           #
################################
# installs xdebug              #
#                              #
# we don't want this in the    # 
# production build because     #
# it will slow down every      #
# single request               #
################################

FROM prod AS dev

RUN install-php-extensions xdebug
