# Camera

使用內建的相機模組拍照或是做影像處理等應用。

## Introduction

Camera 官方有提供照相時，要如何操作 class ， [Camera@Android Developers](http://developer.android.com/reference/android/hardware/Camera.html)

1. Camera.open() 可取得相機物件
2. 使用 getParameters() 取得預設設定值
3. 可修改 Parameters 物件，然後再用 setParameters() 去修改相機的設定
4. 有需要的話，可以呼叫 setDisplayOrientation() 調整相機取樣的方向
5. 相機預覽需要使用 setPreviewDisplay()
6. SurfaceHolder 需要完全初始化
7. 呼叫 startPreview() 即可開始做相機預覽
8. takePicture() 即可做照相的動作
9. 照相完，預覽會停止，如果要繼續啟動相機的話，要再呼叫 startPreview()
10. stopPreview() 可以停止預覽
11. 如果要離開應用程式，必須要呼叫 release() 。可以寫在 onPause() 裡，或是在 onResume() 做重新 open()

### Required Permission

設定 Mainfest.xml 檔，加入以下兩行，第一行是安裝提示要存取 camera 權限，第二行是加入 camera 功能

```xml
<uses-permission android:name="android.permission.CAMERA"/>
<uses-feature android:name="android.hardware.camera" />
```

自動對焦的功能

```xml
<uses-feature android:name="android.hardware.camera.autofocus" />
```

存檔的權限

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

## Flash

此為 API 5 以上的功能。

閃光燈是 Camera 類別的功能,所以必須先建立 Camera 物件再搭配 Camera.Parameters 以控制 Camera 的設定。

開啟閃光燈的範例：

```java
Camera camera;
Parameters parameters;

camera = Camera.open();
parameters = camera.getParameters();
parameters.setFlashMode(Parameters.FLASH_MODE_TORCH);
camera.setParameters(parameters);
```

關閉閃光燈的範例：

```java
parameters.setFlashMode(Parameters.FLASH_MODE_OFF);
camera.setParameters(parameters);
camera.release();
```

切換方法的範例：

```java
String s = p.getFlashMode();
if(s.equals(Parameters.FLASH_MODE_TORCH))
{
    parameters.setFlashMode(Parameters.FLASH_MODE_OFF);
}
else if(s.equals(Parameters.FLASH_MODE_OFF))
{
    parameters.setFlashMode(Parameters.FLASH_MODE_TORCH);
}
```

> **注意：** 關閉或是切換 Activity 時，一樣要 release() ，不然相機功能是不會關閉的。


## Preview

Preview 除了相機拍照可以使用外，也可以用在即時影像處理，如 QR Code 掃描。

通常相機的 preview 都會是全螢幕，所以可以先在 Manifest.xml 宣告 Activity 。

```xml
<activity
    android:name=".PreviewActivity"
    android:theme="@android:style/Theme.Holo.Light.NoActionBar.Fullscreen" />
```

原始來源要 preview 的話，需要一個 SurfaceView 來放它更新的 frames 。

```xml
<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <SurfaceView
        android:id="@+id/preview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</FrameLayout>
</file>
```

Android 預設 preview 的方向是 landscape ，就算設定 portrait ，它的預覽圖依然還是會是用橫向的方式去取圖，並且填滿 SurfaceView。這時可以設定 `setDisplayOrientation(degree)` 解決，取樣的圖會以設的 degree 做順時針旋轉。因此如果要做的像一般照相軟體一樣，翻轉並依它的方向去做拍攝的話，就必需要針對目前方向做調整。

這個問題可以寫 static 的 util 。

```java
public static void setCameraDisplayOrientation(Activity activity, int cameraId, Camera camera) {
    Camera.CameraInfo info = new Camera.CameraInfo();
    Camera.getCameraInfo(cameraId, info);
    int rotation = activity.getWindowManager().getDefaultDisplay().getRotation();
    int degrees = 0;

    switch (rotation) {
        case Surface.ROTATION_0:
            degrees = 0;
            break;
        case Surface.ROTATION_90:
            degrees = 90;
            break;
        case Surface.ROTATION_180:
            degrees = 180;
            break;
        case Surface.ROTATION_270:
            degrees = 270;
            break;
    }

    int result;
    if (info.facing == Camera.CameraInfo.CAMERA_FACING_FRONT) {
        result = (info.orientation + degrees) % 360;
        result = (360 - result) % 360;
    } else {
        result = (info.orientation - degrees + 360) % 360;
    }
    camera.setDisplayOrientation(result);
}
```

References
----------

* [android中Camera setDisplayOrientation使用@小鱼杀上岸](http://www.fish24k.com/?p=655965)
