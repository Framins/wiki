# Model

Rails 的 Model 是使用 ActiveRecord 這個 [[developer:orm]] 元件來操作關聯式資料庫，跟一般 ORM 概念差不多，有以下幾點：

* Class <-> 資料表
* Class method <-> 操作資料表
* Object <-> 個別資料 (Row)
* Object method <-> 操作個別資料
* Object attribute <-> 欄位

產生 model 的指令：

    rails g model [modelName]

產生的檔案：

    invoke  active_record
    create    db/migrate/XXXXXXXXXXXXXX_create_[modelNames].rb
    create    app/models/[modelName].rb
    invoke    test_unit
    create      test/models/[modelName]\_test.rb
    create      test/fixtures/[modelNames].yml

觀察它產生的檔案如下：

  * `migration` 資料庫變動記錄，會有個時間戳記以分辨不同時候的更新 - `db/migrate/XXXXXXXXXXXXXX_create_[modelName].rb`
  * `model` Model 主檔 - `app/models/[modelName].rb`
  * `model_test` Model test - `test/models/[modelName]_test.rb`
  * `fixtures_test` Fixtures - `test/fixtures/[modelName].yml`

Rails 命名慣例：

> Table 名為 Model 名的複數小寫，如果有單字大小寫，會以底線區隔

如果 Rails 英文有錯的話，可以到 `config/initializers/inflections.rb` 修正

再來可以編輯 migration 檔 (假設建立的 model 叫 news)：

```ruby
class CreateNews < ActiveRecord::Migration
  def change
    create_table :news do |t|
      # 這邊開始可以加欄位，格式為 "t.type :columnName"
      t.string :title
      t.string :content
      t.integer :visits

      t.timestamps
    end
    # 這裡可以建立外部鍵
  end
end
```

欄位類型參考：

* integer
* primary_key
* decimal
* float
* boolean
* binary
* string
* text
* date
* time
* datetime
* timestamp

然後執行 `rake db:migrate` 後，就會產生出資料表了：

```
$ rake db:migrate
== XXXXXXXXXXXXXX CreateNews: migrating =======================================
-- create_table(:news)
   -> 0.0404s
== XXXXXXXXXXXXXX CreateNews: migrated (0.0405s) ==============================
```

如果不想用 rails 的命名慣例的話，可以直接修改 `app/models/news.rb` 檔直接指定：

```ruby
class News < ActiveRecord::Base
  self.table_name = "table_name"
  self.primary_key = "primary_key_name"
end
```

建好後，可以用 `rails console` 測試，測完要離開的時候輸入 `exit`

```
# 新增
> news = News.new
> news.title = "test"
> news.content = "第一次玩 ORM"
> news.save # 儲存
> news.id # 主鍵 1，在 Rails 中的主鍵皆為自動遞增的整數 ID

# 新增2
> news = Event.new( :title => "Title2", :content => "第二筆資料")
> news.save
> news.id # 主鍵 2

# 查詢
> news = News.where( :title => "Title2" ).first

# 更新
> news = News.find(1) # 找到主鍵為 1 的資料
> news.content # 輸出 "第一次玩 ORM"
> news.content = "ORM 好好玩"
> news.save # 更新

# 刪除
> news.destroy
```
