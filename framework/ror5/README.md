# Ruby on Rails 5

`Full-stack Framework`

[Ruby on Rails 5][] 應該是目前的最新版，[Ruby][] 要 2.2.2 以上

## Installation

### Mac

先用 brew 安裝 Ruby，預設是 2.3

    brew update
    brew install ruby
    brew link --overwrite ruby

接著用 Gem 安裝 rails 套件

    sudo gem install rails

再來重開終端機應該就會有了

### Docker

使用官方 [`ruby:2.3`](https://hub.docker.com/_/ruby/) 的 image：

    docker run --rm -it -p 3000:3000 ruby:2.3 bash

接著進去後會是 root 身分：

    gem install rails

> `rails new` 會提醒不能用 root 身分，不過 Docker 這個時候通常是拿來測試的，所以可以暫時不理會。

Rails 在啟動內建 server 時（`rails s`），需要依賴 [nodejs](/pdl/node)，所以要再另外安裝

    apt update
    apt install nodejs

嫌麻煩的話，也可以直接使用官方提供的 [`rails`](https://hub.docker.com/_/rails/) image。

## Quick Start

建立新專案

    rails new blog
    # 也可以從即有的目錄建立
    rails new .

開啟測試 server

    cd /path/to/project
    rails s

預設 port 是 3000，打開 http://localhost:3000/ 即可看到預設的測試頁了

[Ruby on Rails 5]: http://rubyonrails.org/
[Ruby]: /pdl/ruby/README.md
