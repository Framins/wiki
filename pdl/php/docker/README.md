Docker Solution
===============

以下都是用官方的 php image 為主，沒特別說明的話就是 Cli/Apache

如果懶得裝 PHP ，可以改 alias

    alias php="docker run -i -t --rm -v \$PWD:/usr/src/app -w /usr/src/app php:7.0-alpine"

Extensions
----------

裝 ext 通常都很不順，少東少西，以下是記錄：

### memcached

    apt-get install libmemcached-dev
    pecl install memcached
    echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini

### soap

    apt-get install libxml2-dev
    docker-php-ext-install soap
