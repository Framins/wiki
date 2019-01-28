# Publishing

Android APK 的上架流程。

## 1. 關閉或移除 logging 和 debugging

* Log
* android:debuggable
* startMethodTracing()
* stopMethodTracing()

## 2. 更新程式的版本設定

檢查 AndroidManifest.xml 裡面的 android:versionCode android:versionName，看是否須修改。

* android:versionCode：給程式判斷使用的，如果是更新 APK，就新增版本號。
* android:versionName：給使用者看的。

## 3. 產生 private key

要放到 Play 上的 APK 必需要先用 private key 簽署過，所以要產生 private key [官方參考資料](http://developer.android.com/tools/publishing/app-signing.html#cert)。

產生的方法有兩種

### 指令產生

使用以下指令：

    keytool -genkey -v -keystore mykey.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000

參數：

* -keystore：檔名，以上例會是 `mykey.keystore` 。
* -alias：別名。
* -validity：有效天數。

### Eclipse 產生

隨著 Eclipse 輸出 APK 的步驟，就會詢問是不是要產生 key 了。

## 4. 在 Eclipse 產生 APK 檔

專案目錄右鍵 -> Android Tools -> Export Signed Application Package...

一、選擇要輸出 APK 的專案。

二、這時就可以選 `Create new keystore` ，即可順便產生新的 private key 。

* Location：選擇產生的 private key 檔案名稱和位置。
* Password：設定密碼(不能小於6個字)。
* Confirm：再輸入一次密碼確認。

三、再來會跟剛剛要產生 private key 的流程一樣

* Alias：別名。
* Password：設定密碼。
* Confirm：再輸入一次密碼。
* Validity (years)：有效期限幾年 (官方建議填 25 年以上)。下面的資料至少填一筆。

四、最後就選 APK 的位置，即可按 finish 輸出了。

## 常見問題

1. 您上傳的 APK 未經壓縮校準，請對您的 APK 執行壓縮校準工具，然後重新上傳。

在 SDK 的目錄裡有個檔案是 `sdk/tools/zipalign.exe` 。要使用此檔來做校準

語法：

    zipalign [-f] [-v] 4 infile.apk outfile.apk

2. 您剛上傳了可偵錯的 APK。基於安全性考量，您必須先停用 APK 的偵錯功能，才能在 Google Play 發佈。

代表 logging 和 debugging 沒有關。

3. 您上傳的 APK 是在偵錯模式下完成簽署，請在發佈模式下簽署 APK。

APK有兩種不同的模式，一種是 debug mode ，另一種是 release mode ，必需要在後者下簽署才能發佈。

References
----------

* [Publishing Overview](http://developer.android.com/tools/publishing/publishing_overview.html)
* [Preparing for Release](http://developer.android.com/tools/publishing/preparing.html)
* [Android APP 上架流程](http://xyz.cinc.biz/2013/06/android-app.html)
