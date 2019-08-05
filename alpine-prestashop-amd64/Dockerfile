FROM yobasystems/alpine:3.10.0-amd64

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Dominic Taylor <dominic@yobasystems.co.uk>" \
    architecture="amd64/x86_64" \
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

RUN echo "@3.9 http://dl-cdn.alpinelinux.org/alpine/v3.9/main" >> /etc/apk/repositories && apk update && \
    apk add php7-common@3.9 php7-fpm@3.9 php7-json@3.9 php7-zlib@3.9 php7-xml@3.9 php7-pdo@3.9 php7-phar@3.9 php7-openssl@3.9 php7-fileinfo@3.9 php7-imagick@3.9 \
    php7-pdo_mysql@3.9 php7-mysqli@3.9 php7-session@3.9 \
    php7-gd@3.9 php7-iconv@3.9 php7-mcrypt@3.9 php7-gmp@3.9 php7-zip@3.9 \
    php7-curl@3.9 php7-opcache@3.9 php7-ctype@3.9 php7-apcu@3.9 php7-memcached@3.9 \
    php7-intl@3.9 php7-bcmath@3.9 php7-dom@3.9 php7-mbstring@3.9 php7-simplexml@3.9 php7-soap@3.9 php7-tokenizer@3.9 php7-xmlreader@3.9 && apk add -u musl && \
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
