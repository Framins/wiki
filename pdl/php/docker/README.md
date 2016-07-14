Docker Solution
===============

以下都是用官方的 php image 為主，沒特別說明的話就是 Cli/Apache

如果懶得裝 PHP ，可以改 alias

    alias php="docker run -i -t --rm -v \$PWD:/usr/src/app -w /usr/src/app php:7.0-alpine"

Extensions
----------

裝 ext 通常都很不順，少東少西，以下是記錄：

### memcached

### soap
