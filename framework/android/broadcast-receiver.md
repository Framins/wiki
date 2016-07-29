# BroadcastReceiver

[BroadcastReceiver](http://developer.android.com/reference/android/content/BroadcastReceiver.html) 跟其他元件比起來，它的特色應該就是被動了。需要傳送訊息給它，它才能有下一步的動作。

BroadcastReceiver 的生命週期只有一個：

* `onReceive(Context, Intent)`

## Register

可以動態地在程式碼裡面新增或是靜態地定義在 [AndroidMainfest.xml](androidmainfest.xml.md)
