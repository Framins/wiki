# Setup on Ubuntu

安裝 Ubuntu Server 並做好更新動作

    sudo apt-get tasksel lamp-server # 安裝LAMP
    sudo apt-get install git-core subversion # 安裝 Git 和 SVN

安裝 rmagick

    sudo apt-get instal imagemagick libmagickcore-dev libmagickwand-dev
    sudo gem install rails
    sudo gem install rmagick

安裝 Passenger

    sudo apt-get install libapache2-mod-passenger

安裝 Redmine

    sudo apt-get install redmine libapache2-mod-fcgid

設定網頁檔案連結

    sudo ln -s /usr/share/redmine/public /var/www/redmine

修改設定檔

    sudo vi /etc/apache2/mods-available/passenger.conf

加入一行

    PassengerDefaultUser www-data

加入網域

    sudo vim /etc/apache2/sites-available/default

加入

```apache
<Directory /var/www/redmine>
  RailsBaseURI /redmine
  PassengerResolveSymlinksInDocumentRoot on
</Directory>
```

開啟模組，重新設定：

    sudo a2enmod passenger
    sudo service apache2 restart

開啟網頁 `http://localhost/redmine`
再來就是Web介面的設定了，使用流程如下：

* 設定帳號，登入帳號：admin，密碼：admin，可修改語言與帳號
* 新增專案
* 設定專案和整合方式
* 開啟帳號
* 角色和權限
* 指派專案人員

## Restart Redmine

網路上通常會有一個很怪的說法叫 restart redmine，它的指令是：

    sudo service restart apache2

## Reference

* [Passenger](https://www.phusionpassenger.com/)
* [Passenger中文說明](http://ihower.tw/rails3/deployment.html)
* [Redmine 安裝紀錄（Ubuntu）](http://lgzenithtech.blogspot.tw/2012/03/redmine-ubuntu.html)
* [將 Redmine 安裝於 Debian、Ubuntu Linux](http://blog.longwin.com.tw/2011/03/redmine-debian-ubuntu-linux-2011/)
* [Ubuntu 10.04 安裝 Redmine](http://blog.darkhero.net/archives/410)
