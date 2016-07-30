Zend_Auth
=========

[Zend_Auth](http://framework.zend.com/manual/1.12/en/zend.auth.html) 是用來驗證使用者的工具，它支援以下的驗證方法 (橋接器的介面：[Zend_Auth_Adapter_Interface](http://framework.zend.com/apidoc/1.12/files/Auth.Adapter.Interface.html))：

* DbTable ([官方說明](http://framework.zend.com/manual/1.12/en/zend.auth.adapter.dbtable.html)，[Zend_Auth_Adapter_DbTable](http://framework.zend.com/apidoc/1.12/files/Auth.Adapter.DbTable.html))
* Digest ([官方說明](http://framework.zend.com/manual/1.12/en/zend.auth.adapter.digest.html)，[ Zend_Auth_Adapter_Digest](http://framework.zend.com/apidoc/1.12/files/Auth.Adapter.Digest.html))
* HTTP ([官方說明](http://framework.zend.com/manual/1.12/en/zend.auth.adapter.http.html)，[Zend_Auth_Adapter_Http](http://framework.zend.com/apidoc/1.12/files/Auth.Adapter.Http.html))
* InfoCard ([Zend_Auth_Adapter_InfoCard](http://framework.zend.com/apidoc/1.12/files/Auth.Adapter.InfoCard.html))
* LDAP ([官方說明](http://framework.zend.com/manual/1.12/en/zend.auth.adapter.ldap.html)，[Zend_Auth_Adapter_Ldap](http://framework.zend.com/apidoc/1.12/files/Auth.Adapter.Ldap.html))
* OpenID ([官方說明](http://framework.zend.com/manual/1.12/en/zend.auth.adapter.openid.html)，[Zend_Auth_Adapter_OpenId](http://framework.zend.com/apidoc/1.12/files/Auth.Adapter.OpenId.html))

驗證後，需要暫存資訊在 Storage 裡，它也提供一個介面[Zend_Auth_Storage_Interface](http://framework.zend.com/apidoc/1.12/files/Auth.Storage.Interface.html)可以繼承，並使用 `setStorage()` 即可做設定。

Zend Framework 對 Storage 有兩個實作：

* [Zend_Auth_Storage_Session](http://framework.zend.com/apidoc/1.12/files/Auth.Storage.Session.html) - 最常見的 Session
* [Zend_Auth_Storage_NonPersistent](http://framework.zend.com/apidoc/1.12/files/Auth.Storage.NonPersistent.html) - 驗證只能是一次性，下次 request 都還是要做驗證的動作

## Basic usage

Zend_Auth使用單例模式實作，取得實例的方法為`Zend_Auth::getInstance()`。

裡面可以操作的方法如下：

|  Method Name  |  Description  |
|  -----------  |  -----------  |
| Zend_Auth_Storage_Interface getStorage() | 取得儲存器，如果沒有設定儲存器的話，預設會new一個`Zend_Auth_Storage_Sessionn`實例 |
| Zend_Auth setStorage(#Zend_Auth_Storage_Interface $storage) | 設定儲存器 |
| Zend_Auth_Result authenticate(#Zend_Auth_Adapter_Interface $adapter) | 驗證 |
| boolean hasIdentity() | 確認是否有登入|
| mixed getIdentity() | 取得登入身份，無登入會回傳null |
| void clearIdentity() | 清除登入身份 |

#### DbTable Adapter

DbTable即為傳統資料表驗證，使用資料表查詢。如果有符合的欄位，即為登入成功。

可以用建構子去設定初值，或是使用setter設定初值

```php
// 建構子
authAdapter = new Zend_Auth_Adapter_DbTable(
    $dbAdapter,
    'users',
    'username',
    'password',
    'MD5(?) AND status = 1'
);

// setter
$authAdapter = new Zend_Auth_Adapter_DbTable($dbAdapter);
$authAdapter
    ->setTableName('users')
    ->setIdentityColumn('username')
    ->setCredentialColumn('password')
    ->setCredentialTreatment($credentialTreatment)
;
```

初始化完後，就可以設定帳號密碼做驗證了

```php
$authAdapter
    ->setIdentity('my_username')
    ->setCredential('my_password')
;

$auth->authenticate($authAdapter);
```

可以取得登入的基本資訊

```php
$authAdapter->getResultRowObject(array('id', 'username', 'nickname'));
```
