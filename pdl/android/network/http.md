# HTTP

## Download ANSI

只適合用在小檔。

記得要加權限：

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

下載流程：

1. New java.net.URL
2. 從 URL 物件建立 HttpURLConnection
3. 從 HttpURLConnection 物件取得 InputStream
4. 從 InputStream 取得資料 (可用 StringBuffer )
5. 取得 SDCard 路徑： Environment.getExternalStorageDirectory()
6. 儲存

## Download Binary

可以用在大檔。

記得要加權限：

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

下載流程：

1. 取得 SDCard 路徑： Environment.getExternalStorageDirectory()
2. 建立對應資料夾，建立文件
3. 用 inputStream 寫入 SDCard
4. 關 stream
