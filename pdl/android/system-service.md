# SystemService

系統級的 Service，以 [Notification](notification.md) 為例，取得的方法如下：

```java
NotificationManager nm = (NotificationManager) getSystemService(NOTIFICATION_SERVICE)
```

每個 Service 和 Class 名稱都有對應，這在[官方說明](http://developer.android.com/reference/android/content/Context.html#getSystemService(java.lang.String) getSystemService() 方法裡面都有寫。

條列如下：

| Class Name | Constant Name | Description | API Level |
| ---------- | ------------- | ----------- | --------- |
| AccessibilityManager | ACCESSIBILITY_SERVICE | | 4 |
| AccountManager | ACCOUNT_SERVICE | | 5 |
| ActivityManager | ACTIVITY_SERVICE | | 1 |
| AlarmManager | ALARM_SERVICE | | 1 |
| AppOpsManager | APP_OPS_SERVICE | | 19 |
| AudioManager | AUDIO_SERVICE | | 1 |
| BluetoothAdapter | BLUETOOTH_SERVICE | | 18 |
| CaptioningManager | CAPTIONING_SERVICE | | 19 |
| ClipboardManager | CLIPBOARD_SERVICE | | 1 |
| ConnectivityManager | CONNECTIVITY_SERVICE | | 1 |
| ConsumerIrManager | CONSUMER_IR_SERVICE | | 19 |
| DevicePolicyManager | DEVICE_POLICY_SERVICE | | 8 |
| DisplayManager | DISPLAY_SERVICE | | 17 |
| framework:android:systemservice:downloadmanager | DOWNLOAD_SERVICE | | 9 |
| DropBoxManager | DROPBOX_SERVICE | | 8 |
| InputMethodManager | INPUT_METHOD_SERVICE | | 3 |
| InputManager | INPUT_SERVICE | | 16 |
| KeyguardManager | KEYGUARD_SERVICE | | 1 |
| LayoutInflater | LAYOUT_INFLATER_SERVICE | | 1 |
| LocationManager | LOCATION_SERVICE | | 1 |
| MediaRouter | MEDIA_ROUTER_SERVICE | | 16 |
| NfcManager | NFC_SERVICE | | 10 |
| [NotificationManager](framework:android:notification) | NOTIFICATION_SERVICE | | 1 |
| NsdManager | NSD_SERVICE | | 16 |
| PowerManager | POWER_SERVICE | | 1 |
| PrintManager | PRINT_SERVICE | | 19 |
| SearchManager | SEARCH_SERVICE | | 1 |
| SensorManager | SENSOR_SERVICE | | 1 |
| StorageManager | STORAGE_SERVICE | | 9 |
| TelephonyManager | TELEPHONY_SERVICE | | 1 |
| TextServicesManager | TEXT_SERVICES_MANAGER_SERVICE | | 14 |
| UiModeManager | UI_MODE_SERVICE | | 8 |
| UsbManager | USB_SERVICE | | 12 |
| UserManager | USER_SERVICE | | 17 |
| WallpaperService | WALLPAPER_SERVICE | | 1 |
| WifiP2pManager | WIFI_P2P_SERVICE | | 14 |
| WifiManager | WIFI_SERVICE | | 1 |
| WindowManager | WINDOW_SERVICE | | 1 |

# DownloadManager

DownloadManager 提供相關的 class 如下：

| Class Name | Description |
| ---------- | ----------- |
| [DownloadManager](http://developer.android.com/reference/android/app/DownloadManager.html) | 下載管理器 |
| [DownloadManager.Query](http://developer.android.com/reference/android/app/DownloadManager.Query.html) | 查詢下載的訊息 |
| [DownloadManager.Request](http://developer.android.com/reference/android/app/DownloadManager.Request.html) | 請求下載的詳細內容 |

## Start

首先要能下載，第一步是需要權限，在 AndroidManifest.xml加入以下權限：

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

DownloadManager 是系統層級的 Service，所以要在 Activity 下用 getSystemService() 取得

```java
DownloadManager downloadManager = (DownloadManager) getSystemService(DOWNLOAD_SERVICE);
```

再來是初始化 Request

```java
String url = "http://www.example.com/file.zip";
DownloadManager.Request request = new DownloadManager.Request(url);
// 設定request
request.setTitle("Title");
request.setDescription("Description");
// 排程下載，並取得唯一碼
long downloadId = downloadManager.enqueue(request);
```

設定 request 的 method 如下，下面每個 method 都可 chaining

| Method | Description |
| ------ | ----------- |
| addRequestHeader(String header, String value) | 設定 HTTP 表頭 |
| setAllowedNetworkTypes(int flags) | 允許下載的網路型態為何，可以為 `NETWORK_MOBILE和NETWORK_WIFI` |
| setAllowedOverMetered(boolean allow) | 是否允許計量網路下載 |
| setAllowedOverRoaming(boolean allowed) | 是否允許漫遊時下載，預設是true |
| setDescription(CharSequence description) | 通知訊息裡的小字 |
| setDestinationInExternalFilesDir(Context context, String dirType, String subPath) | 設定檔案存放位置，使用系統的目錄 |
| setDestinationInExternalPublicDir(String dirType, String subPath) | 設定檔案存放位置，使用自定的目錄 |
| setDestinationUri(Uri uri) | 直接用 Uri 當存檔位置 |
| setMimeType(String mimeType) | 設定檔案的 MimeType。下載完成要開檔案時，即會用這個 MimeType 開啟 |
| setNotificationVisibility(int visibility) | 設定通知列是否顯示 [Android Developer](http://developer.android.com/reference/android/app/DownloadManager.Request.html#setNotificationVisibility(int))有說明傳入值為何 |
| <del>setShowRunningNotification(boolean show)</del> | deprecated in API level 11 |
| setTitle(CharSequence title) | 通知訊息裡的標題 |
| setVisibleInDownloadsUi(boolean isVisible) | 是否要在系統的下載頁面出現 |

在 setNotificationVisibility() 時，設定成 VISIBILITY_HIDDEN 時，要記得加入權限：

```xml
<uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
```

否則會出現錯誤訊息：

    java.lang.SecurityException: Invalid value for visibility: 2
