Ruby on Rails 5
===============

`Full-stack Framework`

[Ruby on Rails 5][] 應該是目前的最新版， [Ruby][] 要 2.2.2 以上

Installation
------------

### Mac

先用 brew 安裝 Ruby ，預設是 2.3

    brew update
    brew install ruby
    brew link --overwrite ruby

接著用 Gem 安裝 rails 套件

    sudo gem install rails

再來重開終端機應該就會有了

Quick Start
-----------

建立新專案

    rails new blog
    # 也可以從即有的目錄建立
    rails new .

開啟測試 server

    cd /path/to/project
    rails s

預設 port 是 3000 ，打開 http://localhost:3000/ 即可看到預設的測試頁了

[Ruby on Rails 5]: http://rubyonrails.org/
[Ruby]: /pdl/ruby/README.md
