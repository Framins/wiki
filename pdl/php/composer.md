# Composer

* [官方原文手冊](https://getcomposer.org/doc/)
* [中文手冊 by Lance](http://getcomposer.ycnets.com/doc/)
* [簡中](http://docs.phpcomposer.com/)
* [COMPOSER設計原理與基本用法](http://blog.turn.tw/?p=1039)
* [Begining Composer](https://speakerdeck.com/jaceju/begining-composer)
* [深入 Composer autoload](https://laravel-china.org/topics/1002)

Composer 可以輕易地解決 PHP 套件下載、安裝、更新、管理等問題。

> Composer 之於 PHP 感覺就很像
> * npm 之於 [Node](/pdl/node/README.md)
> * gem 之於 [Ruby](/pdl/ruby/README.md)
> * pip 之於 [Python](/pdl/python/README.md)

## Installation

    sudo apt-get install curl # 安裝 curl
    curl -sS https://getcomposer.org/installer | php # 產生 composer.phar，然後可以直接執行操作
    sudo mv composer.phar /usr/local/bin/composer # 用全域的方式執行就再下這個指令

[Mac OSX 出錯的解決方法](https://github.com/composer/composer/issues/2839)

### Docker

Add the following statement in `.bash_profile`:

    alias composer="docker run -i -t --rm -v \$PWD:/app composer/composer:1.1-alpine"

> Default PHP version is 7

## Usage

查套件的地方：

https://packagist.org/explore/

## Basic Command

help

    php composer.phar help install

initial

    php composer.phar init
    php composer.phar install

update

    php composer.phar update
    php composer.phar update vendor/package vendor/package2
    php composer.phar update vendor/*

require

    php composer.phar require
    php composer.phar require vendor/package:2.* vendor/package2:dev-master

search

    php composer.phar search monolog

show

    php composer.phar show
    php composer.phar show monolog/monolog
    php composer.phar show monolog/monolog 1.0.2
    php composer.phar show --tree

depends

    php composer.phar depends --tree monolog/monolog

validate

    php composer.phar validate # It will check if your composer.json is valid

status

    php composer.phar status # php composer.phar status -v

self-update

    php composer.phar self-update

config

    php composer.phar config --list

Modifying Repositories

    php composer.phar config repositories.foo vcs http://github.com/foo/bar

create-project

    php composer.phar create-project doctrine/orm path 2.2.0

## Create Package

可以參考 [Packagist](https://packagist.org/) 首頁說明，和 [Composer 語法說明](https://getcomposer.org/doc/04-schema.md)

建立自己的 package，首先要在專案根目錄建立一個 `composer.json` 檔案：

```javascript
{
    "name": "your-vendor-name/package-name",
    "type": "library",
    "description": "A short description of what your package does",
    "keywords": ["log","logging"],
    "homepage": "http://example.com",
    "authors": [
        {
            "name": "Jordi Boggiano",
            "email": "j.boggiano@seld.be",
            "homepage": "http://seld.be",
            "role": "Developer"
        }
    ],
    "require": {
        "php": ">=5.3.0",
        "another-vendor/package": "1.*"
    }
}
```

## Use Private Repositories

[官方說明](https://getcomposer.org/doc/05-repositories.md#hosting-your-own)

* 使用 [Packagist](https://github.com/composer/packagist)
* 使用 [Satis][] 上傳的 repository 記得要標版號，不然就算使用 * 也是找不到的。不過可以用 `dev-master` 來得到最新的 master。[範例](https://github.com/smstw/Development-Tools/issues/1)
* 使用 [Toran Proxy][] (Non-free)

[Satis]: https://github.com/composer/satis
[Toran Proxy]: https://toranproxy.com/
