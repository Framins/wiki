# Setup

最麻煩的安裝...

## Phalcon Extension

### Mac

使用 homebrew 安裝

    brew install php54-phalcon
    brew install php55-phalcon
    brew install php56-phalcon
    brew install php70-phalcon

測試

    echo "<?php echo Phalcon\Version::get() . \"\n\"; ?>" | php
    3.0.0

### Ubuntu

安裝

    sudo apt-get install php5-dev libpcre3-dev gcc make
    git clone --depth=1 git://github.com/phalcon/cphalcon.git
    cd cphalcon/build && git checkout v3.0.0 && ./install
    sudo echo "extension=phalcon.so" > /etc/php5/cli/conf.d/30-phalcon.ini

測試

    echo "<?php echo Phalcon\Version::get() . \"\n\"; ?>" | php
    3.0.0

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

可參考其他人做的 image

* [mileschou/phalcon](https://hub.docker.com/r/mileschou/phalcon/)

或是自己寫 `Dockerfile` 範例：

```dockerfile
FROM php:7.0
MAINTAINER MilesChou <jangconan@gmail.com>

ENV PHALCON_VERSION=3.0.0

# Compile Phalcon
RUN set -xe && \
        curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf v${PHALCON_VERSION}.tar.gz && cd cphalcon-${PHALCON_VERSION}/build && ./install && \
        echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini && \
        cd ../.. && rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION} && \
        # Insall Phalcon Devtools, see https://github.com/phalcon/phalcon-devtools/
        curl -LO https://github.com/phalcon/phalcon-devtools/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf v${PHALCON_VERSION}.tar.gz && \
        mv phalcon-devtools-${PHALCON_VERSION} /usr/local/phalcon-devtools && \
        ln -s /usr/local/phalcon-devtools/phalcon.php /usr/local/bin/phalcon

```

> compile 2.x 時，記憶體需設定 2G 以上才能成功

測試

    docker run -it --rm phalon-image bash
    echo "<?php echo Phalcon\Version::get() . \"\n\"; ?>" | php
    3.0.0

## Phalcon Developer tools

要使用開發者工具前，要先安裝好上面的 [Extension](#Phalcon Extension)。

如果要當全域指令，建議用 [Git](#Git) 下載；如果沒有的話，建議使用 [Composer](#Composer) 下載

### Git

安裝與測試

    $ git clone https://github.com/phalcon/phalcon-devtools
    $ ln -s ./phalcon-devtools/phalcon.php /usr/local/bin/phalcon
    $ phalcon

    Phalcon DevTools (3.0.0)

    Available commands:
      commands         (alias of: list, enumerate)
      controller       (alias of: create-controller)
      module           (alias of: create-module)
      model            (alias of: create-model)
      all-models       (alias of: create-all-models)
      project          (alias of: create-project)
      scaffold         (alias of: create-scaffold)
      migration        (alias of: create-migration)
      webtools         (alias of: create-webtools)

### Composer

定義檔

```javascript
{
    "require": {
        "phalcon/devtools": "3.0.0"
    }
}
```

安裝與測試

    composer install
    php vendor/bin/phalcon.php

    Phalcon DevTools (3.0.0)

    Available commands:
      commands         (alias of: list, enumerate)
      controller       (alias of: create-controller)
      module           (alias of: create-module)
      model            (alias of: create-model)
      all-models       (alias of: create-all-models)
      project          (alias of: create-project)
      scaffold         (alias of: create-scaffold)
      migration        (alias of: create-migration)
      webtools         (alias of: create-webtools)

或是直接裝 global

    composer global require phalcon/devtools=3.0.0
