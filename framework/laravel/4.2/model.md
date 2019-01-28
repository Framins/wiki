# Model

[官方說明](http://laravel.tw/docs/eloquent)

Laravel 使用 Eloquent ORM 來操作 DB

* resource 對應 DB table
* model 對應 row
* 所以 model 是單數，table 是複數
* 而 Eloquent 取得的東西是 Collection

## Relationships

[官方說明](http://laravel.com/docs/4.2/eloquent#relationships)

資料庫難搞的關聯，在 Eloquent ORM 裡設定起來還蠻簡單的，而且還提供幾種比較特別的關聯法

### One To One

比方說，一個 `User` 對應一個 `UserSetting`，可以使用 `hasOne` 方法

```php
class User extends Eloquent {

    public function setting()
    {
        // 使用預設的外鍵 UserSetting.user_id
        return $this->hasOne('UserSetting');
        // 使用自定的外鍵 UserSetting.foreign_key
        // return $this->hasOne('UserSetting', 'userId');
        // 使用自定的外鍵 UserSetting.foreign_key 加上參考到 User.local_key
        // return $this->hasOne('UserSetting', 'foreign_key', 'local_key');
    }
}
```

使用 Dynamic Properties 取得關聯的物件：

```php
$setting = User::find(1)->setting;
```

這行程式碼背後執行的 SQL 如下：

```sql
SELECT * FROM users WHERE id = 1
SELECT * FROM user_settings WHERE user_id = 1
```

相反的，要在 `UserSetting` 定義相對的關聯，可以使用 `belongsTo` 方法：

```php
class UserSetting extends Eloquent {

    public function user()
    {
        // 使用預設的外鍵 UserSetting.user_id
        return $this->belongsTo('User');
        // 使用自定的外鍵 UserSetting.local_key
        // return $this->belongsTo('UserSetting', 'local_key');
        // 使用自定的外鍵 UserSetting.local_key 加上參考到 User.parent_key
        // return $this->belongsTo('UserSetting', 'local_key', 'parent_key');
    }
}
```

### One To Many

比方說，一個 `User` 對應很多 `Post`，可以使用 `hasMany` 方法：

```php
class User extends Eloquent {

    public function posts()
    {
        // 使用預設的外鍵
        return $this->hasMany('Post');

        // 使用自定的外鍵 Post.foreign_key
        // return $this->hasMany('Post', 'foreign_key');
        // 使用自定的外鍵 Post.foreign_key 加上參考到 User.local_key
        // return $this->hasMany('Post', 'foreign_key', 'local_key');
    }
}
```

使用 Dynamic Properties 取得 Post

```php
$posts = User::find(1)->posts;

// 如果要加上條件，可以呼叫方法後再接 where 方法
$posts = User::find(1)->posts()->where('title', '=', 'foo')->first();
```

相反的，要在 `Post` 取得相對的關聯，使用 `belongsTo` 方法：

```php
class Post extends Eloquent {

    public function user()
    {
        return $this->belongsTo('User');
    }
}
```
