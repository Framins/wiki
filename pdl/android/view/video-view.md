# VideoView

VideoView 即是把 SurfaceView 困難的部分都包裝起來，只留其他必要接口給開發者使用。大部分的情況用 VideoView 就可以達到目標需求了。另外再加入 MediaController 就可以完成控制界面了。

## Simple

最簡單的實作，src 打上遠端的 mp4 檔，進入 activity 後就會播放了。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/black" >

    <VideoView
        android:id="@+id/videoView"
        android:layout_centerInParent="true"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</RelativeLayout>
```

> 通常上層 View 都會使用 RelativeLayout，一來是為了要讓子元素能使用 `layout_centerInParent` 屬性置中；另外是通常在載入時，會需要顯示 ProgressBar，而 RelativeLayout 實現重疊的效果相對是比較簡單的。

```java
public class VideoActivity extends Activity {

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_video);

        VideoView videoView = (VideoView) findViewById(R.id.videoView);

        String src = "";
        videoView.setVideoURI(Uri.parse(src));
        videoView.setMediaController(new MediaController(this));
        videoView.requestFocus();
        videoView.start();
    }
}
```

因為是用 URI，所以 src 可以是 http 協定。

MediaController 的建構子，必須要是 Activity 的實例，不能是 getApplicationContext()，這點跟 Dialog 是一樣的。
