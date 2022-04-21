FROM yobasystems/alpine:3.12.12-aarch64

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Dominic Taylor <dominic@yobasystems.co.uk>" \
    architecture="arm64v8/aarch64" \
    nginx-version="1.18.0" \
    php-version="7.3.33" \
    alpine-version="3.12.12" \
    build="21-Apr-2022" \
    org.opencontainers.image.title="alpine-prestashop" \
    org.opencontainers.image.description="Prestashop Docker image running on Alpine Linux" \
    org.opencontainers.image.authors="Dominic Taylor <dominic@yobasystems.co.uk>" \
    org.opencontainers.image.vendor="Yoba Systems" \
    org.opencontainers.image.version="v3.12.12" \
    org.opencontainers.image.url="https://hub.docker.com/r/yobasystems/alpine-prestashop/" \
    org.opencontainers.image.source="https://github.com/yobasystems/alpine-prestashop" \
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
    libmcrypt-dev zlib-dev gmp-dev freetype-dev libjpeg-turbo-dev libpng-dev mysql-client curl \
    php7-common php7-fpm php7-json php7-zlib php7-xml php7-pdo php7-phar php7-openssl php7-fileinfo php7-imagick \
    php7-pdo_mysql php7-mysqli php7-session \
    php7-gd php7-iconv php7-mcrypt php7-gmp php7-zip \
    php7-curl php7-opcache php7-ctype php7-apcu php7-memcached \
    php7-intl php7-bcmath php7-dom php7-mbstring php7-simplexml php7-soap php7-tokenizer php7-xmlreader && apk add -u musl && \
    rm -rf /var/cache/apk/*

RUN sed -i "s/nginx:x:100:101:nginx:\/var\/lib\/nginx:\/sbin\/nologin/nginx:x:100:101:nginx:\/usr:\/bin\/bash/g" /etc/passwd && \
    sed -i "s/nginx:x:100:101:nginx:\/var\/lib\/nginx:\/sbin\/nologin/nginx:x:100:101:nginx:\/usr:\/bin\/bash/g" /etc/passwd- && \
    ln -s /sbin/php-fpm7 /sbin/php-fpm

ADD files/nginx.conf /etc/nginx/
ADD files/php-fpm.conf /etc/php7/
ADD files/php.ini /etc/php7/

ADD files/run.sh /
RUN chmod +x /run.sh

EXPOSE 80
VOLUME ["/usr/html"]

CMD ["/run.sh"]
