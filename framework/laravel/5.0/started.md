# Started

官方建議記憶體 1G 以上，另外 PHP 環境需求：

* PHP >= 5.4
* Mcrypt PHP Extension
* OpenSSL PHP Extension
* Mbstring PHP Extension
* Tokenizer PHP Extension

## PHP Extension

### Ubuntu

使用 apt-get 建置環境

    apt-get install php5-cli php5-json php5-mcrypt

### Vagrant

使用 Vagrant 建置環境

官方有提供 [Homestead](http://laravel.tw/docs/5.0/homestead) 環境

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
      v.memory = 1024
    end
  end
end
```

### Docker

使用 [Docker](/docker) 建置環境，範例：

```dockerfile
FROM php:5.6-fpm

# Install require extension for Laravel
RUN apt-get update -y && apt-get install -y libmcrypt-dev zlib1g-dev && apt-get clean
RUN docker-php-ext-install mbstring mcrypt

# RUN docker-php-ext-install json
# RUN docker-php-ext-install tokenizer

# Install Xdebug 2.3.2 for development
RUN apt-get update -y && apt-get install -y git && apt-get clean
RUN git clone git://github.com/xdebug/xdebug.git /opt/xdebug && \
    cd /opt/xdebug && git checkout XDEBUG_2_3_2 && \
    phpize && \
    ./configure --enable-xdebug && make && \
    cp /opt/xdebug/modules/xdebug.so /usr/local/lib/php/extensions/ && \
    echo "zend_extenstion=/usr/local/lib/php/extensions/xdebug.so" > /usr/local/etc/php/conf.d/ext-xdebug.ini && \
    rm -Rf /opt/xdebug

# Install Composer
RUN apt-get update -y && apt-get install -y curl git zlib1g-dev && apt-get clean
RUN docker-php-ext-install zip
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

CMD ["php-fpm"]
```
