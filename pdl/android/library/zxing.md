# ZXing

ZXing 是一個很多人在使用的條碼掃描器

## Import

Source code 太難搞了，用 Maven 比較簡單，要加的 dependencies 如下

```groovy
compile 'com.google.zxing:android-integration:2.2@jar'
compile 'com.google.zxing:core:2.2@jar'
```

## Required permission

用相機掃的話要加下面的權限

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```

## Start

## Reference

* http://www.getcn.net/?mod=skill&action=detail&id=44041
* http://foonyan.sakura.ne.jp/wisteriahill/QRcode-ZXing/
* [GitHub](https://github.com/zxing/zxing)
* [Play Store Demo](https://play.google.com/store/apps/details?id=com.google.zxing.client.android)
