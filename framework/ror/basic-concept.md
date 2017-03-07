# Basic Concept

一開始可以做的簡單檢查動作

## Create Server

建立新專案的指令：

    rails new helloworld

開測試用伺服器的指令(需在 rails 專案裡面)：

    rails s

## Hello world

以 MVC 規則，需要先有 Controller 來控制 MV 的互動，所以先建立 Controller

    rails generate controller helloworld  # 可簡寫成 rails g controller helloworld

> 執行過程可以參考看看它建了什麼檔案：
>     create  app/controllers/helloworld_controller.rb
>     invoke  erb
>     create    app/views/helloworld
>     invoke  test_unit
>     create    test/controllers/helloworld_controller_test.rb
>     invoke  helper
>     create    app/helpers/helloworld_helper.rb
>     invoke    test_unit
>     create      test/helpers/helloworld_helper_test.rb
>     invoke  assets
>     invoke    coffee
>     create      app/assets/javascripts/helloworld.js.coffee
>     invoke    scss
>     create      app/assets/stylesheets/helloworld.css.scss

由執行過程，可以知道，下 `rails generate controller [controllerName]` 指令的時候，會建以下檔案：

* `controller` 控制器 - `app/controllers/[controllerName]_controller.rb`
* `erb` 樣版目錄(只有目錄) - `app/views/[controllerName]`
* `test_unit` 單元測試 - `test/controllers/[controllerName]_controller_test.rb`
* `helper` Helper - `app/helpers/[controllerName]_helper.rb`
* `helper_test_unit` Helper 的單元測試 - `test/helpers/[controllerName]_helper_test.rb`
* `coffee` Coffee - `app/assets/javascripts/[controllerName].js.coffee`
* `scss` SCSS - `app/assets/stylesheets/[controllerName].css.scss`

再來在路由檔 `config/routes.rb` 加入新設定

```ruby
Helloworld::Application.routes.draw do
    get "helloworld/welcome" => "helloworld#welcome"
end
```

get 的意思就是把 `helloworld/welcome` 對應到 helloworld controller 的 welcome method

現在需要幫 controller 加入 welcome 方法

編輯 `app/controllers/helloworld_controller.rb`

```ruby
class HelloworldController < ApplicationController
    def welcome
    end
end
```

再來要加上 View 的樣版檔： `app/views/helloworld/welcome.html.erb`

```html
<h1>Hello, World!</h1>
```

這樣開啟伺服器後，打 http://localhost:3000/helloworld/welcome 就能看得到內容了。

只是這個 helloworld 並沒有做到 Model 的部分。

## Running mode

在Rails裡有三種執行模式

* development - 開發模式在改 config 或 vender 目錄下的東西需要重新啟動 server
* test
* production - 不管改什麼檔案都需要重新啟動 server
