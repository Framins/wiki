# Setup on Heroku

前置準備：

* 能執行 ubuntu 且能上網的環境，並完成更新 (實體或VM皆可)
* 上 [Heroku](htttp://www.heroku.com/) 申請帳號

## Setup

安裝 `git` `libmagick` `ruby` `libpq`

    apt-get instal git-core libmagickcore-dev ruby libpq-dev

更新 Gem

    gem update

安裝 `RMagick` `Heroku` `Bundler` `pg`

    gem install rmagick heroku bundler pg

Clone Redmine，然後切換到 2.2-stable

    git clone git://github.com/redmine/redmine.git
    cd redmine
    git checkout 2.2-stable

編輯 `.gitignore`，刪除下面幾行

```
Gemfile.lock
Gemfile.local
public/plugin_assets
config/initializers/session_store.rb
config/initializers/secret_token.rb
config/configuration.yml
config/email.yml
```

編輯 `Gemfile`，把 `sqlite` 和 `mysql` 的部分註解掉

```yaml
# Database gems
platforms :mri, :mingw do
  group :postgresql do
    gem "pg", ">= 0.11.0"
  end

#  group :sqlite do
#    gem "sqlite3"
#  end
end

#platforms :mri_18, :mingw_18 do
#  group :mysql do
#    gem "mysql", "~> 2.8.1"
#  end
#end

#platforms :mri_19, :mingw_19 do
#  group :mysql do
#    gem "mysql2", "~> 0.3.11"
#  end
#end
```

修改 `config/application.rb`，在裡面設定值加一行

```ruby
config.assets.initialize_on_precompile = false
```

修改 `config/environment.rb`，下面幾行註解掉

```ruby
# Make sure there's no plugin in vendor/plugin before starting
#vendor_plugins_dir = File.join(Rails.root, "vendor", "plugins")
#if Dir.glob(File.join(vendor_plugins_dir, "*")).any?
#  $stderr.puts "Plugins in vendor/plugins (#{vendor_plugins_dir}) are no longer allowed. " +
#    "Please, put your Redmine plugins in the `plugins` directory at the root of your " +
#    "Redmine directory (#{File.join(Rails.root, "plugins")})"
#  exit 1
#end
```

執行本機安裝

    bundle install
    bundle exec rake generate_secret_token

登入 Heroku，建立 ssh-keys

    heroku login
    heroku keys:add
    heroku create APPNAME

git commit

    git add .
    git commit -m "Prepare for heroku."
    git push heroku 2.2-stable:master

遠端執行安裝指令

    heroku run rake db:migrate
    heroku run rake redmine:load_default_data

最後開瀏覽器打上網址： APPNAME.herokuapp.com 即可看到首頁。
