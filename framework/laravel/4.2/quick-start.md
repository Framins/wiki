# Quick Start

安裝其實還蠻簡單的，不過要用 [Composer][] 才能安裝，另外需要安裝 `php5-mcrypt` 模組：

    apt-get instll php5-mcrypt
    php5enmod mcrypt
    service apache2 restart

使用 composer 直接建立 laravel 專案的方法：

    composer.phar create-project laravel/laravel project

然後要調整 Virtual Host ，設定 root 在 `/path/to/project/public`

* [Apache2](/server/apache.md)

最後記得要把 `app/storage` 設成 apache 可以讀寫的權限，不然會發生[這樣](http://stackoverflow.com/questions/23186952/error-in-exception-handler-laravel)的悲劇。

    chmod 777 /path/to/project/app/storage

[Composer]: /pdl/php/composer.md
