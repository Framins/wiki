# Installation

GitLab 對 Ubuntu 支援度比較高

* [官方 Deb Packages 下載與 VM Images](https://www.gitlab.com/downloads/)
* [官方 Ubuntu 安裝教學](https://github.com/gitlabhq/gitlabhq#installation)
* [官方 Ubuntu 手動安裝教學](https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md)

CentOS

* 官方有 RPM / VM Images
* http://zx1986.github.io/blog/gitlab.html
* https://github.com/gitlabhq/gitlab-recipes/tree/master/install/centos

整合參考：

* [GitLab 6 + Apache + Phusion Passenger](http://k-d-w.org/node/94)

## Packages or Images

這些都打包好了，包括了：

* Ruby
* PostgreSQL
* Redis
* Nginx
* Unicorn
* etc

其中 VM Image 連系統都綁好了，安裝起來就很簡單了。

[預設密碼](#First login)跟手動安裝的一樣

## Ubuntu Installation

參考手動教學一步一步執行的

1. 更新系統：

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```

2. 使用Vim做為預設的編輯器

```bash
sudo apt-get install -y vim
sudo update-alternatives --set editor /usr/bin/vim.basic
```

3. 安裝必要套件

```bash
sudo apt-get install -y build-essential zlib1g-dev libyaml-dev libssl-dev libgdbm-dev libreadline-dev libncurses5-dev libffi-dev curl openssh-server redis-server checkinstall libxml2-dev libxslt-dev libcurl4-openssl-dev libicu-dev logrotate
```

4. 安裝 Git 要 1.7.10 或以上的版本

```bash
sudo apt-get install -y git-core
# git --version
```

5. 如果需要做郵件通知的話，就需要安裝 mail server

```bash
sudo apt-get install -y postfix
```

6. 安裝 Ruby

7. 安裝 Bundler

```bash
sudo gem install bundler --no-ri --no-rdoc
```

8. 建立系統使用者

```bash
sudo adduser --disabled-login --gecos 'GitLab' git
```

9. 安裝GitLab Shell

```bash
# 切換到git目錄
cd /home/git
# Clone原始碼
sudo -u git -H git clone https://gitlab.com/gitlab-org/gitlab-shell.git -b v1.9.1
cd gitlab-shell
sudo -u git -H cp config.yml.example config.yml
# 編輯設定檔，主要是那個gitlab_url
sudo -u git -H editor config.yml
# 安裝
sudo -u git -H ./bin/install
```

10. 資料庫

GitLab 是建議用 PostgreSQL。

```bash
sudo apt-get install -y postgresql-9.1 postgresql-client libpq-dev
sudo -u postgres psql -d template1
# SQL操作
template1=# CREATE USER git;
template1=# CREATE DATABASE gitlabhq_production OWNER git;
template1=# \q
# 測試
# sudo -u git -H psql -d gitlabhq_production
```

11. 安裝GitLab

前置作業都完成了，現在要開始安裝 GitLab 了

```bash
cd /home/git
sudo -u git -H git clone https://gitlab.com/gitlab-org/gitlab-ce.git -b 6-7-stable gitlab
cd /home/git/gitlab
```

再來可以在裡面切換想要安裝的版本，官方是不建議在正式執行的環境用 master，好怪的設定....

調整設定

```bash
cd /home/git/gitlab
# 複製範例設定檔來用
sudo -u git -H cp config/gitlab.yml.example config/gitlab.yml
# 確認url正確
sudo -u git -H editor config/gitlab.yml

# 確保GitLab可以寫入log和tmp目錄
sudo chown -R git log/
sudo chown -R git tmp/
sudo chmod -R u+rwX  log/
sudo chmod -R u+rwX  tmp/

# 建立目錄給satellites
sudo -u git -H mkdir /home/git/gitlab-satellites

# 建立sockets和pids目錄
sudo -u git -H mkdir tmp/pids/
sudo -u git -H mkdir tmp/sockets/
sudo chmod -R u+rwX  tmp/pids/
sudo chmod -R u+rwX  tmp/sockets/

# 建立上傳目錄
sudo -u git -H mkdir public/uploads
sudo chmod -R u+rwX  public/uploads

# 複製Unicorn的設定範例
sudo -u git -H cp config/unicorn.rb.example config/unicorn.rb

# 調效設定以應付高負載時的情況
# Ex. change amount of workers to 3 for 2GB RAM server
sudo -u git -H editor config/unicorn.rb

# Copy the example Rack attack config
sudo -u git -H cp config/initializers/rack_attack.rb.example config/initializers/rack_attack.rb

# 設定Git的全域設定
sudo -u git -H git config --global user.name "GitLab"
sudo -u git -H git config --global user.email "gitlab@localhost"
sudo -u git -H git config --global core.autocrlf input
```

再來是要設定 Database

```bash
# 複製postgresql的設定範例
sudo -u git cp config/database.yml.postgresql config/database.yml
# Mysql
# sudo -u git cp config/database.yml.mysql config/database.yml

# 調整登入使用者設定
sudo -u git -H editor config/database.yml

# 改成唯讀
sudo -u git -H chmod o-rwx config/database.yml
```

12. 安裝 Gems

```bash
cd /home/git/gitlab

# For PostgreSQL (note, the option says "without ... mysql")
sudo -u git -H bundle install --deployment --without development test mysql aws

# Or if you use MySQL (note, the option says "without ... postgres")
sudo -u git -H bundle install --deployment --without development test postgres aws
```

13. 初始化資料庫

```bash
sudo -u git -H bundle exec rake gitlab:setup RAILS_ENV=production
# 說 yes
```

14. 安裝開始自動執行

```bash
sudo cp lib/support/init.d/gitlab /etc/init.d/gitlab
sudo cp lib/support/init.d/gitlab.default.example /etc/default/gitlab
sudo update-rc.d gitlab defaults 21
```

設定 logrotate

```bash
sudo cp lib/support/logrotate/gitlab /etc/logrotate.d/gitlab
```

確認程式狀態

```bash
sudo -u git -H bundle exec rake gitlab:env:info RAILS_ENV=production
```

開啟服務

```bash
sudo service gitlab start
# or
# sudo /etc/init.d/gitlab restart
```

編譯

```bash
sudo -u git -H bundle exec rake assets:precompile RAILS_ENV=production
```

### Nginx

安裝

```bash
sudo apt-get install -y nginx
```

設定

```bash
sudo cp lib/support/nginx/gitlab /etc/nginx/sites-available/gitlab
sudo ln -s /etc/nginx/sites-available/gitlab /etc/nginx/sites-enabled/gitlab

# Change YOUR_SERVER_FQDN to the fully-qualified
# domain name of your host serving GitLab.
sudo editor /etc/nginx/sites-available/gitlab
```

重新啟動

```bash
sudo service nginx restart
```

### 完成

再次確定

```bash
sudo -u git -H bundle exec rake gitlab:check RAILS_ENV=production
```

### First login

```
root
5iveL!fe
```
