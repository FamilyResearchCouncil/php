FROM php:7.4-fpm AS prod

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

FROM base AS dev

RUN install-php-extensions xdebug
