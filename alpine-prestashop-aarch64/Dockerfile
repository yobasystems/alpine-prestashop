FROM yobasystems/alpine:3.8.1-aarch64
LABEL maintainer "Dominic Taylor <dominic@yobasystems.co.uk>" architecture="ARM64v8/aarch64" alpineversion="3.8.1" build="26-nov-2018"
LABEL nginx-version="1.14.1" php-version="7.2.10" prestashop-version="latest"

ENV REPO="https://github.com/PrestaShop/PrestaShop" \
    SSH_PRIVATE_KEY="" \
    URL="www.example.co.uk" \
    PS_FOLDER_ADMIN="admin" \
    PS_FOLDER_INSTALL="install" \
    PS_INSTALL_AUTO="0" \
    PS_ERASE_DB="0" \
    PS_INSTALL_GIT="0" \
    TERM="xterm" \
    MYSQL_HOST="172.17.0.1" \
    MYSQL_DATABASE="" \
    MYSQL_USER=""\
    MYSQL_PASSWORD=""

RUN apk update && \
    apk add bash less vim nginx ca-certificates git tzdata zip \
    libmcrypt-dev zlib-dev gmp-dev \
    freetype-dev libjpeg-turbo-dev libpng-dev \
    php7-fpm php7-json php7-zlib php7-xml php7-pdo php7-phar php7-openssl php7-fileinfo php7-imagick \
    php7-pdo_mysql php7-mysqli php7-session \
    php7-gd php7-iconv php7-mcrypt php7-gmp php7-zip \
    php7-curl php7-opcache php7-ctype php7-apcu \
    php7-intl php7-bcmath php7-dom php7-mbstring php7-simplexml php7-xmlreader mysql-client curl && apk add -u musl && \
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
VOLUME ["/usr"]

CMD ["/run.sh"]
