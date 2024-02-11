# Prestashop container image running on Alpine Linux

[![Docker Automated build](https://img.shields.io/docker/automated/yobasystems/alpine-prestashop.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-prestashop/)
[![Docker Pulls](https://img.shields.io/docker/pulls/yobasystems/alpine-prestashop.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-prestashop/)
[![Docker Stars](https://img.shields.io/docker/stars/yobasystems/alpine-prestashop.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-prestashop/)

[![Alpine Version](https://img.shields.io/badge/Alpine%20version-v3.19.0-green.svg?style=for-the-badge)](https://alpinelinux.org/)
[![Prestashop Version](https://img.shields.io/badge/Prestashop%20version-v8.1.3-green.svg?style=for-the-badge)](https://www.prestashop.com/en)


This Docker image [(yobasystems/alpine-prestashop)](https://hub.docker.com/r/yobasystems/alpine-prestashop/) is based on the minimal [Alpine Linux](https://alpinelinux.org/) ready for running [Prestashop](https://www.prestashop.com/en). (Requires external database)

### Alpine Version 3.19.0 (Released 2023-12-07)
##### Prestashop Version 8.1.3
##### PHP Version 8.1.27
##### Nginx Version 1.24.0

----

## What is Alpine Linux?
Alpine Linux is a Linux distribution built around musl libc and BusyBox. The image is only 5 MB in size and has access to a package repository that is much more complete than other BusyBox based images. This makes Alpine Linux a great image base for utilities and even production applications. Read more about Alpine Linux here and you can see how their mantra fits in right at home with Docker images.

## What is Prestashop?
PrestaShop is an efficient and innovative e-commerce solution with all the features you need to create an online store and grow your business.

## Features

* Minimal size only 75 MB and only 16 layers
* Memory usage is minimal on a simple install

## Architectures

* ```:amd64```, ```:x86_64``` - 64 bit Intel/AMD (x86_64/amd64)
* ```:arm64v8```, ```:aarch64``` - 64 bit ARM (ARMv8/aarch64)
* ```:arm32v7```, ```:armhf``` - 32 bit ARM (ARMv7/armhf)

##### PLEASE CHECK TAGS BELOW FOR SUPPORTED ARCHITECTURES, THE ABOVE IS A LIST OF EXPLANATION

## Tags

* ```:latest``` latest branch based (Automatic Architecture Selection)
* ```:master``` master branch usually inline with latest
* ```:amd64```, ```:x86_64```  amd64 based on latest tag but amd64 architecture
* ```:aarch64```, ```:arm64v8``` Armv8 based on latest tag but arm64 architecture
* ```:armhf```, ```:arm32v7``` Armv7 based on latest tag but arm32 architecture

## Layers & Sizes

![Version](https://img.shields.io/badge/version-amd64-blue.svg?style=for-the-badge)
![MicroBadger Layers (tag)](https://img.shields.io/docker/layers/yobasystems/alpine-prestashop/amd64.svg?style=for-the-badge)
![MicroBadger Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-prestashop/amd64.svg?style=for-the-badge)

![Version](https://img.shields.io/badge/version-aarch64-blue.svg?style=for-the-badge)
![MicroBadger Layers (tag)](https://img.shields.io/docker/layers/yobasystems/alpine-prestashop/aarch64.svg?style=for-the-badge)
![MicroBadger Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-prestashop/aarch64.svg?style=for-the-badge)

![Version](https://img.shields.io/badge/version-armhf-blue.svg?style=for-the-badge)
![MicroBadger Layers (tag)](https://img.shields.io/docker/layers/yobasystems/alpine-prestashop/armhf.svg?style=for-the-badge)
![MicroBadger Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-prestashop/armhf.svg?style=for-the-badge)


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
docker exec <image_id> apk add php81-soap
docker restart <image_name>
```

```
php81-common
php81-pdo_sqlite
php81-pear
php81-ftp
php81-imap
php81-mysqli
php81-json
php81-mbstring
php81-soap
php81-litespeed
php81-sockets
php81-bcmath
php81-opcache
php81-dom
php81-zlib
php81-gettext
php81-fpm
php81-intl
php81-openssl
php81-session
php81-mcrypt
php81-pdo_mysql
php81-embed
php81-xmlrpc
php81-wddx
php81-dba
php81-ldap
php81-xsl
php81-exif
php81-pdo_dblib
php81-bz2
php81-pdo
php81-pspell
php81-sysvmsg
php81-gmp
php81-apache2
php81-pdo_odbc
php81-shmop
php81-ctype
php81-phpdbg
php81-enchant
php81-sysvsem
php81-sqlite3
php81-odbc
php81-pcntl
php81-calendar
php81-xmlreader
php81-snmp
php81-zip
php81-posix
php81-iconv
php81-curl
php81-doc
php81-gd
php81-xml
php81-dev
php81-cgi
php81-sysvshm
php81-pgsql
php81-tidy
php81-pdo_pgsql
php81-phar
php81-mysqlnd
```

## Docker Compose example:

```yalm
prestashop:
  image: yobasystems/alpine-prestashop
  environment:
    VIRTUAL_HOST: example.co.uk
    MYSQL_DATABASE: prestadb
    MYSQL_PASSWORD: prestapass
    MYSQL_ROOT_PASSWORD: ''
    MYSQL_USER: prestauser
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

## Source Repositories

* [Github - yobasystems/alpine-prestashop](https://github.com/yobasystems/alpine-prestashop)

* [Gitlab - yobasystems/alpine-prestashop](https://gitlab.com/yobasystems/alpine-prestashop)

* [Bitbucket - yobasystems/alpine-prestashop](https://bitbucket.org/yobasystems/alpine-prestashop/)


## Container Registries

* [Dockerhub - yobasystems/alpine-prestashop](https://hub.docker.com/r/yobasystems/alpine-prestashop/)

* [Quay.io - yobasystems/alpine-prestashop](https://quay.io/repository/yobasystems/alpine-prestashop)


## Links

* [Yoba Systems](https://www.yobasystems.co.uk/)

* [Github - Yoba Systems](https://github.com/yobasystems/)

* [Dockerhub - Yoba Systems](https://hub.docker.com/u/yobasystems/)

* [Quay.io - Yoba Systems](https://quay.io/organization/yobasystems)

* [Maintainer - Dominic Taylor](https://github.com/dominictayloruk)

## Donation

[![BMAC](https://img.shields.io/badge/BUY%20ME%20A%20COFFEE-£5-blue.svg?style=for-the-badge&logo=buy-me-a-coffee)](https://www.buymeacoffee.com/dominictayloruk?new=1)

[![BITCOIN](https://img.shields.io/badge/BTC-bc1q7hy8qmyvq7rw6slrna7yffcdnj9rcg4e9xjecc-blue.svg?style=for-the-badge&logo=bitcoin)](bitcoin:bc1q7hy8qmyvq7rw6slrna7yffcdnj9rcg4e9xjecc)

[![ETHEREUM](https://img.shields.io/badge/ETH-0xb6bE2e4da3d86b50Bdae1F9B6960c23dd87C532C-blue.svg?style=for-the-badge&logo=ethereum)](ethereum:0xb6bE2e4da3d86b50Bdae1F9B6960c23dd87C532C)