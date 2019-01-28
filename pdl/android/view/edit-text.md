# EditText

[官方說明](http://developer.android.com/reference/android/widget/EditText.html)

繼承如下：

* java.lang.Object
  * android.view.View
    * android.widget.TextView
      * android.widget.EditText

基本上 XML 屬性都是繼承 TextView 的

| Attribute | Description |
| --------- | ----------- |
| android:hint | String Resource，輸入框在沒有值的時候，會出現的提示 |
| android:numeric | Keyword，數字的格式，可以為以下常數值： integer, signed, decimal |
| android:singleLine | Boolean，設定 true 後，就會變單行模式了 |
| android:password | Boolean，設定 true 後，輸入會變密碼 |
| android:capitalize | Keyword，可轉大小寫 |
| android:ellipsize | Keyword，指定溢位隱藏的方式 |

## android:imeOptions

鍵盤最右下角的功能鍵樣式。有以下 Keyword 可選：

| Keyword | Description |
| ------- | ----------- |
| actionUnspecified | 預設，無特別指定 |
| actionNone | 沒有動作 |
| actionGo | 去往 |
| actionSearch | 搜索 |
| actionSend | 發送 |
| actionNext | 下一個 |
| actionDone | 完成 |

## android:inputType

此屬性，會改變虛擬鍵盤的樣式或是內容識別的方法。有以下 Keyword 可選：

| Keyword | Description |
| ------- | ----------- |
| none | 預設，無特別指定 |
| text | 普通文字 |
| textCapCharacters | 大寫文字 |
| textCapWords | 單字的首字母大寫 |
| textCapSentences | 只有第一個字母大寫 |
| textAutoCorrect | 自動完成 |
| textAutoComplete | 自動完成 |
| textMultiLine | 多行輸入 |
| textImeMultiLine | 輸入法多行 |
| textNoSuggestions | 不提示 |
| textUri | 網址格式 |
| textEmailAddress | 電子信箱格式 |
| textEmailSubject | 電子信箱主題 |
| textShortMessage | 短訊息 |
| textLongMessage | 長訊息 |
| textPersonName | 人名 |
| textPostalAddress | 地址 |
| textPassword | 密碼 |
| textVisiblePassword | 可見密碼 |
| textWebEditText | 網頁表單 |
| textFilter | |
| textPhonetic | 拼音輸入 |
| number | 數字 |
| numberSigned | 帶號數字 |
| numberDecimal | 帶小數點的數字|
| phone | 撥號鍵盤 |
| datetime | 日期時間 |
| date | 日期鍵盤 |
| time | 時間鍵盤 |
