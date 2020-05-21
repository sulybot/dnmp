FROM php:fpm-alpine

# software resouce mirror for alpine apk
ARG ALPINE_PACKAGE_REPO_MIRROR

# default timezone
ARG TZ=Asia/Shanghai

ARG PHP_EXTENSIONS

# php.ini config {development|production}
ARG PHP_INI_ENV=development

# php-fpm uid & gid, default 1000, the primary user of host
ARG UID=1000
ARG GID=1000

RUN sed -i "s/dl-cdn.alpinelinux.org/${ALPINE_PACKAGE_REPO_MIRROR}/g" /etc/apk/repositories

RUN if [ "${TZ}" != "" ]; then \
        apk --no-cache add tzdata git; \
        cp "/usr/share/zoneinfo/$TZ" /etc/localtime; \
        echo "$TZ" > /etc/timezone; \
    fi

ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions $PHP_EXTENSIONS && \
    cp "$PHP_INI_DIR/php.ini-${PHP_INI_ENV}" "$PHP_INI_DIR/php.ini" && \
    sed -i "s#;date\.timezone\s=#date.timezone = ${TIME_ZONE}#g" "$PHP_INI_DIR/php.ini"

ENV COMPOSER_HOME=/tmp/composer

RUN curl -o /usr/bin/composer https://mirrors.aliyun.com/composer/composer.phar \
    && chmod +x /usr/bin/composer && /usr/bin/composer config -g repo.packagist composer https://packagist.phpcomposer.com

RUN apk --no-cache add shadow && usermod -u ${UID} www-data && groupmod -g ${GID} www-data
