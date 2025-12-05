# Prestashop container image running on Alpine Linux

[![Docker Automated build](https://img.shields.io/docker/automated/yobasystems/alpine-prestashop.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-prestashop/)
[![Docker Pulls](https://img.shields.io/docker/pulls/yobasystems/alpine-prestashop.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-prestashop/)
[![Docker Stars](https://img.shields.io/docker/stars/yobasystems/alpine-prestashop.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-prestashop/)

[![Alpine Version](https://img.shields.io/badge/Alpine%20version-v3.23.0-green.svg?style=for-the-badge)](https://alpinelinux.org/)
[![Prestashop Version](https://img.shields.io/badge/Prestashop%20version-v9.0.1-green.svg?style=for-the-badge)](https://www.prestashop.com/en)

This Container image [(yobasystems/alpine-prestashop)](https://hub.docker.com/r/yobasystems/alpine-prestashop/) is based on the minimal [Alpine Linux](https://alpinelinux.org/) ready for running [Prestashop](https://www.prestashop.com/en). (Requires external database)

### Alpine Version 3.23.0 (Released 2025-12-03)

##### Prestashop Version 9.0.1

##### PHP Version 8.4.15

##### Nginx Version 1.28.0

---

## What is Alpine Linux?

Alpine Linux is a Linux distribution built around musl libc and BusyBox. The image is only 5 MB in size and has access to a package repository that is much more complete than other BusyBox based images. This makes Alpine Linux a great image base for utilities and even production applications. Read more about Alpine Linux here and you can see how their mantra fits in right at home with Container images.

## What is Prestashop?

PrestaShop is an efficient and innovative e-commerce solution with all the features you need to create an online store and grow your business.

## Features

- Minimal size only 75 MB and only 16 layers
- Memory usage is minimal on a simple install

## Architectures

- `:amd64`, `:x86_64` - 64 bit Intel/AMD (x86_64/amd64)
- `:arm64v8`, `:aarch64` - 64 bit ARM (ARMv8/aarch64)
- `:arm32v7`, `:armhf` - 32 bit ARM (ARMv7/armhf)

##### PLEASE CHECK TAGS BELOW FOR SUPPORTED ARCHITECTURES, THE ABOVE IS A LIST OF EXPLANATION

## Tags

- `:latest` latest branch based (Automatic Architecture Selection)
- `:main` main branch usually inline with latest
- `:amd64`, `:x86_64` amd64 based on latest tag but amd64 architecture
- `:aarch64`, `:arm64v8` Armv8 based on latest tag but arm64 architecture
- `:armhf`, `:arm32v7` Armv7 based on latest tag but arm32 architecture

## 📏 Layers & Sizes

![Version](https://img.shields.io/badge/version-amd64-blue.svg?style=for-the-badge)
![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-prestashop/amd64.svg?style=for-the-badge)

![Version](https://img.shields.io/badge/version-aarch64-blue.svg?style=for-the-badge)
![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-prestashop/aarch64.svg?style=for-the-badge)

![Version](https://img.shields.io/badge/version-armhf-blue.svg?style=for-the-badge)
![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-prestashop/armhf.svg?style=for-the-badge)

## Creating an instance

### Upload limit

The upload limit is 128 Megabytes.

### Environment variables

- SSH_PRIVATE_KEY=""
- URL="example.com"
- PS_FOLDER_ADMIN="admin"
- PS_FOLDER_INSTALL="install"
- PS_INSTALL_AUTO="0"
- PS_ERASE_DB="0"
- PS_INSTALL_GIT="0"
- CLOUDFLARE_CDN="0"
- DEV_MODE="0"
- TERM="xterm"
- MYSQL_HOST="mariadb:3306"
- MYSQL_DATABASE="prestashop"
- MYSQL_USER="prestashop"
- MYSQL_PASSWORD="prestashop"

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
docker exec <image_id> apk add php84-soap
docker restart <image_name>
```

```
php84-common
php84-pdo_sqlite
php84-pear
php84-ftp
php84-imap
php84-mysqli
php84-json
php84-mbstring
php84-soap
php84-litespeed
php84-sockets
php84-bcmath
php84-opcache
php84-dom
php84-zlib
php84-gettext
php84-fpm
php84-intl
php84-openssl
php84-session
php84-mcrypt
php84-pdo_mysql
php84-embed
php84-xmlrpc
php84-wddx
php84-dba
php84-ldap
php84-xsl
php84-exif
php84-pdo_dblib
php84-bz2
php84-pdo
php84-pspell
php84-sysvmsg
php84-gmp
php84-apache2
php84-pdo_odbc
php84-shmop
php84-ctype
php84-phpdbg
php84-enchant
php84-sysvsem
php84-sqlite3
php84-odbc
php84-pcntl
php84-calendar
php84-xmlreader
php84-snmp
php84-zip
php84-posix
php84-iconv
php84-curl
php84-doc
php84-gd
php84-xml
php84-dev
php84-cgi
php84-sysvshm
php84-pgsql
php84-tidy
php84-pdo_pgsql
php84-phar
php84-mysqlnd
```

## Docker Compose example:

```yaml
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
  image: yobasystems/alpine-prestashop
```

## 📚 Source Repositories

- [Github - yobasystems/alpine-prestashop](https://github.com/yobasystems/alpine-prestashop)
- [Gitlab - yobasystems/alpine-prestashop](https://gitlab.com/yobasystems/alpine-prestashop)

## 🐳 Container Registries

- [Dockerhub - yobasystems/alpine-prestashop](https://hub.docker.com/r/yobasystems/alpine-prestashop/)
- [Quay.io - yobasystems/alpine-prestashop](https://quay.io/repository/yobasystems/alpine-prestashop)
- [GHCR - yobasystems/alpine-prestashop](https://ghcr.io/yobasystems/alpine-prestashop)

## 🔗 Links

- [Yoba Systems](https://yoba.systems/)
- [Github - Yoba Systems](https://github.com/yobasystems/)
- [Dockerhub - Yoba Systems](https://hub.docker.com/u/yobasystems/)
- [Quay.io - Yoba Systems](https://quay.io/organization/yobasystems)
- [GHCR - Yoba Systems](https://ghcr.io/yobasystems)
- [Maintainer - Dominic Taylor](https://github.com/dominictayloruk)
