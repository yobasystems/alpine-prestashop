# Prestashop Docker image running on Alpine Linux

[![Docker Layers](https://img.shields.io/badge/docker%20layers-16-blue.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-prestashop/) [![Docker Size](https://img.shields.io/badge/docker%20size-75%20MB-blue.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-prestashop/) [![Docker Stars](https://img.shields.io/docker/stars/yobasystems/alpine-prestashop.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-prestashop/) [![Docker Pulls](https://img.shields.io/docker/pulls/yobasystems/alpine-prestashop.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-prestashop/)

[![Alpine Version](https://img.shields.io/badge/alpine%20version-v3.8.1-green.svg?maxAge=2592000?style=flat-square)](http://alpinelinux.org/) [![Prestashop Version](https://img.shields.io/badge/Prestashop%20version-vlatest-green.svg?maxAge=2592000?style=flat-square)](https://www.prestashop.com/en)


This Docker image [(yobasystems/alpine-prestashop)](https://hub.docker.com/r/yobasystems/alpine-prestashop/) is based on the minimal [Alpine Linux](http://alpinelinux.org/) ready for running [Prestashop](https://www.prestashop.com/en). (Requires external database)

##### Alpine Version 3.8.1 (Released September 11, 2018)
##### Prestashop Version latest
##### PHP Version 7.2.10
##### Nginx Version 1.14.1

----

## What is Alpine Linux?
Alpine Linux is a Linux distribution built around musl libc and BusyBox. The image is only 5 MB in size and has access to a package repository that is much more complete than other BusyBox based images. This makes Alpine Linux a great image base for utilities and even production applications. Read more about Alpine Linux here and you can see how their mantra fits in right at home with Docker images.

## What is Prestashop?
PrestaShop is an efficient and innovative e-commerce solution with all the features you need to create an online store and grow your business.

## Features

* Minimal size only 75 MB and only 16 layers
* Memory usage is minimal on a simple install
* Memory usage is around 100mb on a simple install.

## Architectures

* ```:amd64```, ```:latest``` - 64 bit Intel/AMD (x86_64/amd64)
* ```:i386```, ```:x86``` - 32 bit Intel/AMD (x86/i686)
* ```:arm64v8```, ```:aarch64``` - 64 bit ARM (ARMv8/aarch64)
* ```:arm32v7```, ```:armhf``` - 32 bit ARM (ARMv7/armhf)

#### PLEASE CHECK TAGS BELOW FOR SUPPORTED ARCHITECTURES, THE ABOVE IS A LIST OF EXPLANATION

## Tags

* ```:latest```, ```:amd64``` latest branch based on amd64
* ```:master``` master branch usually inline with latest
* ```:v0.0.0``` version number related to docker version
* ```:armhf```, ```:arm32v7``` Armv7 based on latest tag but arm architecture

## Creating an instance


### Upload limit

The upload limit is 128 Megabytes.

### Change php.ini value
modify files/php-fpm.conf

To modify php.ini variable, simply edit php-fpm.ini and add php_flag[variable] = value.

```
php_flag[display_errors] = on
```

### PHP Modules
#### List of available modules in Alpine Linux, not all these are installed.
##### In order to install a php module do, (leave out the version number i.e. -5.6.11-r0
```
docker exec <image_id> apk add <pkg_name>
docker restart <image_name>
```
Example:

```
docker exec <image_id> apk add php7-soap
docker restart <image_name>
```

```
php7-common
php7-pdo_sqlite
php7-pear
php7-ftp
php7-imap
php7-mysqli
php7-json
php7-mbstring
php7-soap
php7-litespeed
php7-sockets
php7-bcmath
php7-opcache
php7-dom
php7-zlib
php7-gettext
php7-fpm
php7-intl
php7-openssl
php7-session
php7-mcrypt
php7-pdo_mysql
php7-embed
php7-xmlrpc
php7-wddx
php7-dba
php7-ldap
php7-xsl
php7-exif
php7-pdo_dblib
php7-bz2
php7-pdo
php7-pspell
php7-sysvmsg
php7-gmp
php7-apache2
php7-pdo_odbc
php7-shmop
php7-ctype
php7-phpdbg
php7-enchant
php7-sysvsem
php7-sqlite3
php7-odbc
php7-pcntl
php7-calendar
php7-xmlreader
php7-snmp
php7-zip
php7-posix
php7-iconv
php7-curl
php7-doc
php7-gd
php7-xml
php7-dev
php7-cgi
php7-sysvshm
php7-pgsql
php7-tidy
php7-pdo_pgsql
php7-phar
php7-mysqlnd
```

## Docker Compose example:

```yalm
prestashop:
  image: yobasystems/alpine-prestashop
  environment:
    VIRTUAL_HOST: example.co.uk
  expose:
    - "80"
  volumes:
    - /data/example/www:/usr/html
  restart: always
  links:
    - mysql:mysql
mysql:
  environment:
    MYSQL_DATABASE: prestadb
    MYSQL_PASSWORD: prestapass
    MYSQL_ROOT_PASSWORD: ''
    MYSQL_USER: prestauser
  image: yobasystems/alpine-mariadb
```

## Source Repository

* [Bitbucket - yobasystems/alpine-prestashop](https://bitbucket.org/yobasystems/alpine-prestashop/)

* [Github - yobasystems/alpine-prestashop](https://github.com/yobasystems/alpine-prestashop)

## Links

* [Yoba Systems](https://www.yobasystems.co.uk/)

* [Dockerhub - yobasystems](https://hub.docker.com/u/yobasystems/)

* [Quay.io - yobasystems](https://quay.io/organization/yobasystems)
