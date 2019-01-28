Vagrant
=======

Vagrant 的重點：

* 協助安裝、設定虛擬機
* 也可以儲存在發佈
* 專為開發者設計，以虛擬機為主的開發環境
* 自動化，可程式化
* 可攜性

Start
-----

支持開源，所以用 [VirtualBox](https://www.virtualbox.org/) + [Vagrant](https://www.vagrantup.com/) 來做 start

Mac 也可以用 brew 下載安裝

```bash
brew cask install vagrant      --appdir=/Application
brew cask install virtualbox   --appdir=/Application
```

建虛擬機，[OS list](http://www.vagrantbox.es/) ：

```bash
mkdir demo
cd demo
vagrant init ubuntu/trusty64  # 這道指令會去下載 box 檔
vagrant up
```

現在虛擬機啟動了，只要在同個目錄下，都可以 ssh 進去

```bash
vagrant ssh
```

也可以關機

```bash
vagrant halt
```

或是從 VirtualBox 的清單中移除

```bash
vagrant destory
```

halt + up + take effect changed in the Vagrantfile

```bash
vagrant reload [name|id]
```

Force the provisioners to run

```bash
vagrant provision [vm-name] 
```

Vagrantfile
-----------

Vagrant 在啟動 box 之前，需要先定義好要啟動的是哪一種 box 和定義相關屬性，如

* VM 的名稱
* 檔案的 URL
* 分配的記憶體
* port 對應關係

我們可以在選定的工作目錄裡，把這些屬性寫到一個叫 `Vagrantfile` 的設定檔裡，它是用 Ruby 寫的。

這 box 是用哪個 repository

```ruby
config.vm.box = "ubuntu/trusty64"
```

Port forwarding 可以建立 host port 與 guest port 間的連結，比方說 host 的 8080 要導到虛擬機的 80 ：

```ruby
config.vm.network "forwarded_port", guest: 80, host: 8080
```

Private network 其實就是 host-only，另外可以設定 IP，VM 間也是用這個 IP 在溝通

```ruby
config.vm.network "private_network", ip: "192.168.33.10"
```

Public network 是使用 bridged network 直接接到外部網路

```ruby
config.vm.network "public_network"
```

共享目錄，比方說工作目錄下的 `www` 要對應虛擬機的 `/var/www/html` ：

```ruby
config.vm.synced_folder "www", "/var/www/html"
```

設定 VirtualBox 中顯示的名稱和記憶體大小

```ruby
config.vm.customize ["modifyvm", :id, "--name", "redis", "--memory", "512"]
```

Basic
-----

看本機端的 Vagrant repository

```bash
vagrant box list
```

看目前 Vagrant 的狀態

```bash
vagrant status
```

當 box 內容初始化差不多了，就可以用打包指令，在未來的時候可以使用：

```bash
vagrant package --output redis.box
```

打包後的東西可以再匯入到 Vagrant repository 裡

```bash
$ vagrant box add --name new-demo redis.box
```

只要有 Vagrant repository 裡面有的，就可以拿來 init 出一個新的虛擬機

```bash
vagrant init new-demo
```

Reference
---------

* http://www.codedata.com.tw/social-coding/vagrant-tutorial-1-developer-and-vm/
* http://gogojimmy.net/2013/05/26/vagrant-tutorial/
* http://www.slideshare.net/ihower/vagrant-osdc
