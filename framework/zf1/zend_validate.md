# Zend_Validate

[Zend_Validate](http://framework.zend.com/manual/1.12/en/zend.validate.html) 可以驗證輸入內容是否符合規則。

Zend 預設的驗證方法：

| Class Name | Description |
| ---------- | ----------- |
| Zend_Validate_EmailAddress | 驗證 Email 規則 |
| Zend_Validate_StringLength | 字串長度 |

## Usage

所有的驗證方法都會繼承 `Zend_Validate_Interface`。而這介面裡會有兩個方法： `isValid()` and `getMessages()`

此為官方的基本實作例子

```php
$validator = new Zend_Validate_EmailAddress();

if ($validator->isValid($email)) {
    // email appears to be valid
} else {
    foreach ($validator->getMessages() as $messageId => $message) {
        echo "Validation failure '$messageId': $message\n";
    }
}
```

自定訊息有時需要取得原輸入的文字做說明，可以用 `%value%` 表示之。

```php
$validator = new Zend_Validate_StringLength(array('min' => 8, 'max' => 12));

$validator->setMessages(array(
    Zend_Validate_StringLength::TOO_SHORT => 'The string \'%value%\' is too short',
    Zend_Validate_StringLength::TOO_LONG  => 'The string \'%value%\' is too long'
));

if (!$validator->isValid("test")) {
    $messages = $validator->getMessages();
    echo current($messages); // 這裡測過，使用 current 是可以正確地取到的
}
```

如果要取得判斷值的話，可能需要參考原 class 是否有提供。
