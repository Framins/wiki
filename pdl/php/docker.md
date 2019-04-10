# Docker Solution

以下都是用官方的 php image 為主，沒特別說明的話就是 Cli/Apache

如果懶得裝 PHP，可以改 alias

    alias php="docker run -i -t --rm -v \$PWD:/usr/src/app -w /usr/src/app php:7.0-alpine"

## Extensions

裝 ext 通常都很不順，少東少西，以下是記錄：

### memcache

5.6 以下的版本： 

    apt-get install -y zlib1g-dev
    pecl install memcache
    echo "extension=memcache.so" > /usr/local/etc/php/conf.d/memcache.ini

7.0 以上的版本需使用[其他人改出來的函式庫](https://github.com/websupport-sk/pecl-memcache)：

    curl -LOs https://github.com/websupport-sk/pecl-memcache/archive/php7.tar.gz
    tar zxf php7.tar.gz
    cd pecl-memcache-php7 && phpize && ./configure --enable-memcache && make && make install
    echo "extension=memcache.so" > /usr/local/etc/php/conf.d/memcache.ini

### memcached

    apt-get install -y libmemcached-dev
    pecl install memcached
    echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini

### mongodb

    apt-get install -y libssl-dev 
    pecl install mongodb
    echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini

### soap

    apt-get install -y libxml2-dev
    docker-php-ext-install soap

### zip

    apt-get install -y zlib1g-dev
    docker-php-ext-install zip

### xdebug

7.1

    pecl install xdebug
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

7.0

    pecl install xdebug
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20151012/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

5.6

    pecl install xdebug
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini 

5.x

    pecl install xdebug
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20121212/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini 

## Troubleshooting

### Docker 官方 PHP 5.5 版無法使用 `apt-get update`

下面是一個 workaround 方法，[參考網站](https://unix.stackexchange.com/questions/508724/failed-to-fetch-jessie-backports-repository/508791)  

```dockerfile
RUN sed -i '/deb http:\/\/httpredir.debian.org\/debian jessie-updates main/d' /etc/apt/sources.list

RUN apt-get update
```
