# Started

## Ubuntu

懶人包使用 `rvm` 一行指令安裝 ​[Rails Girls - Installation scripts](https://github.com/railsgirls/installation-scripts/blob/master/rails-install-ubuntu.sh)

* 要用使用者權限安裝，用 `sudo` 它會裝到全域資料夾裡，然後就會噴錯
* 安裝的時候，如果 `.bashrc` 已經有設定 `$PATH` 的話會噴錯
* 裝完要[調整設定](https://rvm.io/integration/gnome-terminal)，記得重開終端機
* 不知道為何沒有裝到 `rails` ，需要再下一次 `gem install rails --no-rdoc --no-ri` 指令才會安裝

## Common

* 設定 git 相關環境
* 安裝 node.js ， rails 啟動內建伺服器必須

伺服器，看需求再選擇裝哪一種，目前大部分就是 Apache 和 Nginx 的選擇，再搭配 [Passenger](https://www.phusionpassenger.com/) 即可

    sudo apt-get install -y apache2 libapache2-mod-ruby  # 安裝 Aapche 和 mod_ruby
    sudo a2enmod rewrite                                 # 需開啟 mod_rewrite
    sudo apt-get build-dep nginx                         # Nginx

資料庫，本機開發可以使用 SQLite ，上線可以換 MySQL 或 PostgreSQL ，看需求再選擇裝哪一種

    sudo apt-get install mysql-server mysql-clinet libmysql++-dev libdbi-ruby libdbd-mysql-ruby  # MySQL
    sudo apt-get install sqlite3 libsqlite3-dev  # SQLite
    sudo apt-get install libpq-dev postgresql-client postgresql pgadmin3  # PostgreSQL

    -u postgres psql postgres password postgres                      # 設定postgres的密碼
    -u postgres createdb mydb                                        # 建立一個database

Rmagick

    apt-get install imagemagick graphicsmagick-libmagick-dev-compat libmagickwand-dev

Redis

## apt

安裝軟體：

* Ruby 1.9.3
* Rails 3.2.13
* Rubygems 1.8.23

這應該是最簡單的了， Ubuntu 都已經處理好了。

    sudo apt-get install ruby ruby-dev rails rubygems rake # 安裝相關套件
    sudo apt-get install vim-rails # Vim 外掛

如果沒裝 ruby-dev 的話， gem 更新可能會出現錯誤： ERROR: Failed to build gem native extension.

### RVM

[RVM](http://www.openfoundry.org/tw/tech-column/8513-rvm-ruby-environment-version-manager) 提供同一環境下安裝多個 Ruby 版本，先安裝必要套件：

    sudo apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev libxml2-dev libxslt-dev autoconf libc6-dev

user 目錄下安裝 rvm ，並安裝 Ruby 2.0 ：

    curl -L https://get.rvm.io | bash -s stable
    source ~/.rvm/scripts/rvm
    rvm autolibs enable
    rvm install 2.0.0 # 安裝 2.0.0 版的 Ruby
    rvm list # 看目前使用哪一版的 Ruby
    rvm use 2.0.0 # 使用 2.0.0 版
    rvm --default use 2.0.0 # 設定預設 Ruby 版本
    rvm rubygems current # 安裝 Rubygems

## Gem

Gem 是一個 Ruby 的套件管理系統，就跟 Ubuntu 的 apt 一樣，預設會安裝到系統裡。

常用指令

    gem list -r [name]           # 尋找一個叫 [name] 的套件
    gem cleanup                  # 清除 cache
    gem install [name]           # 安裝 [name]
    gem uninstall [name]         # 移除 [name]
    gem list --local             # 看 local 裝了什麼 package

安裝 rails 和資料庫軟體

    gem install rails -v=3.2.14   # 安裝 Rails
    gem install sqlite3           # 安裝 Ruby 與 SQLite 的 Apapter
    gem install ruby-mysql        # 安裝 Ruby 與 MySQL 的 Apapter
    gem install pg                # 安裝 Ruby 與 PostgreSQL 的 Apapter

## Testing

以上安裝完成後，就可以來實際測試了，下指令：

    rails new helloworld     # 建立 helloworld 專案資料夾
    cd helloworld
    rails s                  # 打開伺服器，進去目錄後執行才能開啟 Rails 內帶的伺服器

記得預設的 port 會是 3000 。如果上面都沒做錯的話，等一回兒可以開瀏覽器觀看剛剛建的網頁了。

# Reference

* http://billy3321.blogspot.tw/2013/09/ubuntu-1304-serverruby-on-rails-app.html
* http://pm.5fpro.com/projects/public-wiki/wiki/Ubuntu_-_Ruby_on_Rails
* http://blog.wu-boy.com/2014/02/ruby-with-nginx-on-ubuntu-debian/
* http://ihower.tw/rails3/installation.html
* http://blog.longwin.com.tw/2008/11/ruby-on-rails-linux-environment-build-2008/
