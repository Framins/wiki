# Apache

## .htaccess

開啟方法，首先要找到 apache 設定目錄的地方，然後在類似下面這樣的 section：

```apache
<Directory />
    Options FollowSymLinks
    AllowOverride All   # 這裡改成 All 即可套用在這個目錄設定下
</Directory>
```

`AllowOverride` 的意思是允許用 `.htaccess` 去覆寫原本 `apache` 的設定。

參考：

## Virtual Host

Name-based virtual host example

```apache
NameVirtualHost *:80

<VirtualHost *:80>
DocumentRoot /var/www/example1
ServerName www.example.com
</VirtualHost>

<VirtualHost *:80>
DocumentRoot /var/www/example2
ServerName www.example.org
</VirtualHost>
```

Note: `NameVirtualHost` 好像只能接 IP ，不能接 domain...

## Reference

* http://www.htaccesseditor.com/ - 線上做 `.htaccess` ，沒想到連這種東西也有...
* [.htaccess - Wiki](http://en.wikipedia.org/wiki/.htaccess)
* [官方範例](http://httpd.apache.org/docs/2.0/vhosts/examples.html)
* [鳥哥的 Apache](http://linux.vbird.org/linux_server/0360apache.php)
