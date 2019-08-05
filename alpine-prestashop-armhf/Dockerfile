FROM yobasystems/alpine:3.10.0-armhf

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Dominic Taylor <dominic@yobasystems.co.uk>" \
    architecture="arm32v7/armhf" \
    nginx-version="1.16.0" \
    php-version="7.2.19" \
    alpine-version="3.10.0" \
    build="05-Aug-2019" \
    org.opencontainers.image.title="alpine-prestashop" \
    org.opencontainers.image.description="Prestashop Docker image running on Alpine Linux" \
    org.opencontainers.image.authors="Dominic Taylor <dominic@yobasystems.co.uk>" \
    org.opencontainers.image.vendor="Yoba Systems" \
    org.opencontainers.image.version="v3.10.0" \
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
    TERM="xterm" \
    MYSQL_HOST="172.17.0.1" \
    MYSQL_DATABASE="" \
    MYSQL_USER="" \
    MYSQL_PASSWORD=""

RUN apk update && \
    apk add bash less vim geoip nginx nginx-mod-http-headers-more nginx-mod-http-geoip nginx-mod-stream nginx-mod-stream-geoip ca-certificates git tzdata zip \
    libmcrypt-dev zlib-dev gmp-dev freetype-dev libjpeg-turbo-dev libpng-dev mysql-client curl

RUN echo "@threepointnine http://dl-cdn.alpinelinux.org/alpine/v3.9/main" >> /etc/apk/repositories && apk update && \
    apk add php7-common@threepointnine php7-fpm@threepointnine php7-json@threepointnine php7-zlib@threepointnine php7-xml@threepointnine php7-pdo@threepointnine php7-phar@threepointnine php7-openssl@threepointnine php7-fileinfo@threepointnine php7-imagick@threepointnine \
    php7-pdo_mysql@threepointnine php7-mysqli@threepointnine php7-session@threepointnine \
    php7-gd@threepointnine php7-iconv@threepointnine php7-mcrypt@threepointnine php7-gmp@threepointnine php7-zip@threepointnine \
    php7-curl@threepointnine php7-opcache@threepointnine php7-ctype@threepointnine php7-apcu@threepointnine php7-memcached@threepointnine \
    php7-intl@threepointnine php7-bcmath@threepointnine php7-dom@threepointnine php7-mbstring@threepointnine php7-simplexml@threepointnine php7-soap@threepointnine php7-tokenizer@threepointnine php7-xmlreader@threepointnine && apk add -u musl && \
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
