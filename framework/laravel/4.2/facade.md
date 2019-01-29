# Facade

Facade 感覺像是提供一個靜態的介面，然後從這個介面去存取 IoC 裡的物件。用靜態的原因應該是 coding style 和 DI 兩個原因。

官方的說明實在是太抽象了，所以上網去找了別的資料，然後再整理起來

假設最後的實體 class 名叫： `Member/Config`

## Step 1

建立一個類別 `app/facades/Member/Config.php`

```php
namespace Member;

class Config {
    public function getConfig() {
        return array();
    }
}
```

這個檔案需要放在 Composer 知道該如何自動載入的目錄，因為目錄是自定義，所以要在 `composer.json` 加入自動載入的位置：

```json
"autoload": {
    "psr-0": {
        "Member": "app/facades"
    }
}
```

## Step 2

建立 Facade class `app/facades/Member/Facades/Config.php`，此 class 必須繼承 `Illuminate\Support\Facades\Facade`，並要寫一個 `protected static function getFacadeAccessor()` 它回傳的 IoC 綁定的名稱。

```php
namespace Member\Facades;
use Illuminate\Support\Facades\Facade;
class Config extends Facade {
    protected static function getFacadeAccessor() {
        return 'MemberConfig';
    }
}
```

## Step 3

建立 ServiceProvider class `app/facades/Member/ConfigServiceProvider.php`，需繼承 `Illuminate\Support\ServiceProvider`。

```php
namespace Member;

use Illuminate\Support\ServiceProvider;

class ConfigServiceProvider extends ServiceProvider {
    public function register() {
        $this->app->bindShared('MemberConfig', function ($app) {
            return new \Member\Config();
        });
    }
}
```

在 `app/config/app.php` 註冊 ServiceProvider 與設定別名

```php
'providers' => array(
    'Member\ConfigServiceProvider',
),

'aliases' => array(
    'MemberConfig' => 'Member\Facades\Config',
},
```

## Step 4

到此為止就完成了，最後只要用下面程式碼就能執行第一個實體 class 了。

```php
MemberConfig::getConfig();
```

## References

* http://laravel.tw/docs/facades
* http://www.yuansir-web.com/2014/08/13/laravel-%E5%88%9B%E5%BB%BA-facades-%E5%AE%9E%E4%BE%8B/
