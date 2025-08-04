FROM yobasystems/alpine:3.22.1-aarch64

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Dominic Taylor <dominic@yoba.systems>" \
    architecture="arm64v8/aarch64" \
    nginx-version="1.28.0" \
    php-version="8.1.32" \
    alpine-version="3.22.1" \
    build="03-Aug-2025" \
    org.opencontainers.image.title="alpine-prestashop" \
    org.opencontainers.image.description="Prestashop container image running on Alpine Linux" \
    org.opencontainers.image.authors="Dominic Taylor <dominic@yoba.systems>" \
    org.opencontainers.image.vendor="Yoba Systems" \
    org.opencontainers.image.version="3.22.1" \
    org.opencontainers.image.url="https://hub.docker.com/r/yobasystems/alpine-prestashop/" \
    org.opencontainers.image.source="https://github.com/yobasystems/alpine-prestashop" \
    org.opencontainers.image.base.name="docker.io/yobasystems/alpine:3.22.1" \
    org.opencontainers.image.revision=$VCS_REF \
    org.opencontainers.image.created=$BUILD_DATE

ENV REPO="https://github.com/PrestaShop/PrestaShop" \
    SSH_PRIVATE_KEY="" \
    URL="www.example.co.uk" \
    PS_FOLDER_ADMIN="admin" \
    PS_FOLDER_INSTALL="install" \
    PS_INSTALL_AUTO="0" \
    PS_ERASE_DB="0" \
    PS_INSTALL_GIT="0" \
    CLOUDFLARE_CDN="0" \
    DEV_MODE="0" \
    TERM="xterm" \
    MYSQL_HOST="172.17.0.1" \
    MYSQL_DATABASE="" \
    MYSQL_USER="" \
    MYSQL_PASSWORD=""

RUN apk update && \
    apk --no-cache add bash less vim geoip nginx nginx-mod-http-headers-more nginx-mod-http-geoip nginx-mod-stream nginx-mod-stream-geoip ca-certificates git tzdata zip \
    libmcrypt-dev zlib-dev gmp-dev freetype-dev libjpeg-turbo-dev libpng-dev mysql-client curl musl

RUN apk --no-cache \
    --repository=https://dl-cdn.alpinelinux.org/alpine/v3.19/community \
    --repository=https://dl-cdn.alpinelinux.org/alpine/v3.19/main \
    add \
    icu-libs \
    php81-common php81-fpm php81-json php81-zlib php81-xml php81-pdo php81-phar php81-openssl php81-fileinfo \
    php81-pdo_mysql php81-mysqli php81-session \
    php81-gd php81-iconv php81-gmp php81-zip \
    php81-curl php81-opcache php81-ctype php81-apcu \
    php81-intl php81-bcmath php81-dom php81-mbstring php81-simplexml php81-soap php81-tokenizer php81-xmlreader php81-pecl-imagick php81-pecl-memcached \
    rm -rf /var/cache/apk/*

RUN sed -i "s/nginx:x:100:101:nginx:\/var\/lib\/nginx:\/sbin\/nologin/nginx:x:100:101:nginx:\/usr:\/bin\/bash/g" /etc/passwd && \
    sed -i "s/nginx:x:100:101:nginx:\/var\/lib\/nginx:\/sbin\/nologin/nginx:x:100:101:nginx:\/usr:\/bin\/bash/g" /etc/passwd- && \
    ln -s /sbin/php-fpm81 /sbin/php-fpm

ADD files/nginx.conf /etc/nginx/
ADD files/php-fpm.conf /etc/php81/
ADD files/php.ini /etc/php81/

ADD files/run.sh /
RUN chmod +x /run.sh

EXPOSE 80
VOLUME ["/usr/html"]

CMD ["/run.sh"]
