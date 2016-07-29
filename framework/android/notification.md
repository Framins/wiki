# Notification

Android 在有訊息要通知使用者的時候，會在狀態列上出現訊息。

[Notification](http://developer.android.com/reference/android/app/Notification.html) 的功能就是要來操作這些訊息該如何呈現的。

## Build

Notification 在 API level 11 之前都是使用建構子產生實例，再設定屬性的。

    Notification(int icon, CharSequence tickerText, long when)

> 從 API level 11 開始，改用 [Notification.Builder](http://developer.android.com/reference/android/app/Notification.Builder.html) 建構。  
> 從 API level 16 開始，改用 `build` 取得 Notification Object 。

```java
Notification notification = new Notification.Builder(mContext)
        .setContentTitle("Title")
        .setContentText("Text")
        .setSmallIcon(R.drawable.small_icon)
        .setLargeIcon(R.drawable.large_icon)
        .build();
```

Notification.Builder 可以用的 Method 可以參考 [API](#API)

> **注意:** `setSmallIcon()` 是必要要設定的，不然它不會理你。

## API

| Method Name | Description | Remark |
| ----------- | ----------- | ------ |
| addAction(int icon, CharSequence title, PendingIntent intent) | 新增Action | Added in API level 16 |
| setAutoCancel(boolean autoCancel) | 自動取消 | |
| setContent(RemoteViews views) | 設定自定View | |
| setContentInfo(CharSequence info) | 設定右下角的小文字 | |
| setContentIntent(PendingIntent intent) | 在點擊通知的時候，會發出的PendingIntent | |
| setContentText(CharSequence text) | 設定通知第二行的內文 | |
| setContentTitle(CharSequence title) | 設定通知第一行的標題文字 | |
| setDefaults(int defaults) | 設定預設提醒方式 | DEFAULT_SOUND：聲音提醒、DEFAULT_VIBRATE：震動、DEFAULT_LIGHTS：閃光、DEFAULT_ALL：全部 |
| setDeleteIntent(PendingIntent intent) | 在手動通知時，會發出的PendingIntent | |
| setExtras(Bundle bag) | | Added in API level 19 |
| setFullScreenIntent(PendingIntent intent, boolean highPriority) | | |
| setLargeIcon(Bitmap icon) | | |
| setLights(int argb, int onMs, int offMs) | 設定前置LED的閃爍方式 | 參數依序為：顏色、亮的時間、暗的時間 |
| setNumber(int number) | | |
| setOngoing(boolean ongoing) | 設定true時，通知就不能移除。預設為false | |
| setOnlyAlertOnce(boolean onlyAlertOnce) | | |
| setPriority(int pri) | | Added in API level 16 |
| setProgress(int max, int progress, boolean indeterminate) | 當設定這個屬性時，就會有進度條顯示 | indeterminate參數如果true代表是不確定進度的狀況；如果要設progress，就要設false |
| setShowWhen(boolean show) | | Added in API level 17 |
| setSmallIcon(int icon, int level) | | |
| setSmallIcon(int icon) | | |
| setSound(Uri sound) | 設定提醒的鈴聲 | |
| setSound(Uri sound, int streamType) | 設定提醒的鈴聲 | |
| setStyle(Notification.Style style) | | Added in API level 16 |
| setSubText(CharSequence text) | 第三行文字 | Added in API level 16 |
| setTicker(CharSequence tickerText, RemoteViews views) | 第一次通知的時候，會顯示文字在狀態列上 | |
| setTicker(CharSequence tickerText) | 第一次通知的時候，會顯示文字在狀態列上 | |
| setUsesChronometer(boolean b) | | Added in API level 16 |
| setVibrate(long[] pattern) | 設定震動的方式 | 陣列第一個數字是停止時間、第二個數字是震動時間，第三個數字開始就是一直循環。 |
| setWhen(long when) | | |

前置 LED 的權限：

```xml
<uses-permission android:name="android.permission.FLASHLIGHT"/>
```

震動器的權限：

```xml
<uses-permission android:name="android.permission.VIBRATE"/>
```
