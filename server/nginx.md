# Nginx

[Nginx](http://nginx.org/)，是個強調高效能和低記憶體使用率的 httpd。

## HTTP

HTTP config example for development:

```
http {
    #...

    # 上傳檔案最大的大小
    client_max_body_size 128m;
    #...
}
```

## VirtualHost

Example for development:

```
server {
    listen 80;

    root /home/vagrant/hostname/public;
    index index.html index.htm index.php;

    server_name hostname;

    location / {
        # 加這個才會傳參數進去 php
        try_files $uri $uri/ =404 /index.php$is_args$args;

        # 開發者不需要 cache 啦 (摔
        expires off;
    }

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;

        # for Zend Framework
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param APPLICATION_ENV development;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

## SSL

相關資料可以wiki

[建立參考網站](http://blog.gtwang.org/linux/nginx-create-and-install-ssl-certificate-on-ubuntu-linux/)

1. 建立一個放置憑證的目錄 `sudo mkdir /etc/nginx/ssl`
2. 使用 `openssl` 產生自行簽署的 SSL 憑證 `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt`

參數與簡略說明：

* req：使用 X.509 Certificate Signing Request（CSR） Management 產生憑證。
* -x509：建立自行簽署的憑證。
* -nodes：不要使用密碼保護，因為這個憑證是 NGINX 伺服器要使用的，如果設定密碼的話，會讓伺服器每次在啟動時書需要輸入密碼。
* -days 365：設定憑證的使用期限，單位是天，如果不想時常重新產生憑證，可以設長一點。
* -newkey rsa:2048：同時產生新的 RSA 2048 位元的金鑰。
* -keyout：設定金鑰儲存的位置。
* -out：設定憑證儲存的位置。

設定 NGINX 伺服器，在原本的設定檔中加上 SSL 的設定，並且設定憑證與金鑰的路徑：

```
server {
  listen 80 default_server;
  listen [::]:80 default_server;

  # 加入 SSL 設定
  listen 443 ssl default_server;
  listen [::]:443 ssl default_server;

  # 憑證與金鑰的路徑
  ssl_certificate /etc/nginx/ssl/nginx.crt;
  ssl_certificate_key /etc/nginx/ssl/nginx.key;

  # ...
}
```

## With PHP-FPM

Ubuntu 12.04

* http://www.lonelycoder.be/nginx-php-fpm-mysql-phpmyadmin-on-ubuntu-12-04/

## LNMP

* https://www.linode.com/docs/websites/nginx/nginx-and-phpfastcgi-on-ubuntu-12-04-lts-precise-pangolin
* http://lnmp.org/install.html
* http://www.binarytides.com/install-nginx-php-fpm-mariadb-debian/
