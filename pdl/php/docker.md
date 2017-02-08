Docker Solution
===============

以下都是用官方的 php image 為主，沒特別說明的話就是 Cli/Apache

如果懶得裝 PHP ，可以改 alias

    alias php="docker run -i -t --rm -v \$PWD:/usr/src/app -w /usr/src/app php:7.0-alpine"

Extensions
----------

裝 ext 通常都很不順，少東少西，以下是記錄：

### memcache

5.6 以下的版本： 

    apt-get install zlib1g-dev
    pecl install memcache
    echo "extension=memcache.so" > /usr/local/etc/php/conf.d/memcache.ini

7.0 以上的版本需使用[其他人改出來的函式庫](https://github.com/websupport-sk/pecl-memcache)：

    curl -LOs https://github.com/websupport-sk/pecl-memcache/archive/php7.tar.gz
    tar zxf php7.tar.gz
    cd pecl-memcache-php7 && phpize && ./configure --enable-memcache && make && make install
    echo "extension=memcache.so" > /usr/local/etc/php/conf.d/memcache.ini

### memcached

    apt-get install libmemcached-dev
    pecl install memcached
    echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini

### soap

    apt-get install libxml2-dev
    docker-php-ext-install soap

### zip

    apt-get install zlib1g-dev
    docker-php-ext-install zip

### xdebug

7.0

    pecl install xdebug
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20151012/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini 

5.6

    pecl install xdebug
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini 

5.x

    pecl install xdebug
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20121212/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini 
