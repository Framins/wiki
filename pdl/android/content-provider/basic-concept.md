# Basic Concept

基本上 ContentProvider 可以看作是一個網站，可以使用 Uri 取得資料。如 Android 取得聯絡人資料的 Uri 為：

```
content://com.android.contacts/contacts
```

其中前面 `content://` 為 Android 規定的 scheme，中間的 `com.android.contacts` 稱為 [Authority](http://developer.android.com/guide/topics/manifest/provider-element.html)，有點類似網站主機。\\
最後的 `contacts` 則是路徑(Path)。

而上面只是一個字串，必需要轉換成 Uri 物件，才能讓 ContentProvider 做處理；想把字串轉成 Uri 物件的方法：

```java
Uri uri = Uri.parse("content://com.android.contacts/contacts");
```
