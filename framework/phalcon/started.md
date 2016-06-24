# Started

最麻煩的安裝...

## Phalcon Extension

### Mac

使用 homebrew 安裝

    brew install php54-phalcon
    brew install php55-phalcon
    brew install php56-phalcon

測試

    echo "<?php echo Phalcon\Version::get() . \"\n\"; ?>" | php
    2.0.0

### Ubuntu

安裝

    sudo apt-get install php5-dev libpcre3-dev gcc make
    git clone --depth=1 git://github.com/phalcon/cphalcon.git
    cd cphalcon/build && ./install
    sudo echo "extension=phalcon.so" > /etc/php5/cli/conf.d/30-phalcon.ini

測試

    echo "<?php echo Phalcon\Version::get() . \"\n\"; ?>" | php
    2.0.0

### Vagrant

使用 Vagrant 建置環境

官方有提供 [Vagrant](https://github.com/phalcon/vagrant) 環境版

也可以配合上面 [Ubuntu](#Ubuntu) 安裝 script

```ruby
Vagrant.configure(2) do |config|
  config.vm.define :web do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.host_name = "web"
    config.vm.synced_folder ".", "/vagrant"
    config.vm.network "private_network", ip: "10.10.10.10"
    config.vm.provision "shell", path: "scripts/install.sh"

    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
    end
  end
end
```

### Docker

使用 Docker 建置環境，範例：

```dockerfile
ROM php:5.6-apache
MAINTAINER MilesChou <jangconan@gmail.com>

# Install require extension
RUN apt-get update -y && apt-get install -y git && apt-get clean && rm -r /var/lib/apt/lists/*

RUN git clone git://github.com/phalcon/cphalcon.git /usr/local/src/cphalcon;\
    cd /usr/local/src/cphalcon/build && git checkout phalcon-v2.0.9 && ./install ;\
    echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini
```

> 用 Vagrant 測試過，記憶體需設定 2G 以上才能 compile

## Phalcon Developer tools

要使用開發者工具前，要先安裝好上面的 [Extension](#Phalcon Extension) 。

如果要當全域指令，建議用 [Git](#Git) 下載；如果沒有的話，建議使用 [Composer](#Compose) 下載

### Git

安裝與測試


    git clone https://github.com/phalcon/phalcon-devtools
    ./phalcon-devtools/phalcon.sh

    Phalcon DevTools (2.0.0)

    Available commands:
      commands (alias of: list, enumerate)
      controller (alias of: create-controller)
      model (alias of: create-model)
      all-models (alias of: create-all-models)
      project (alias of: create-project)
      scaffold (alias of: create-scaffold)
      migration (alias of: create-migration)
      webtools (alias of: create-webtools)

### Composer

定義檔

```javascript
{
    "require": {
        "phalcon/devtools": "dev-master"
    }
}
```

安裝與測試

    composer install
    php vendor/bin/phalcon.php

    Phalcon DevTools (2.0.0)

    Available commands:
      commands (alias of: list, enumerate)
      controller (alias of: create-controller)
      model (alias of: create-model)
      all-models (alias of: create-all-models)
      project (alias of: create-project)
      scaffold (alias of: create-scaffold)
      migration (alias of: create-migration)
      webtools (alias of: create-webtools)
