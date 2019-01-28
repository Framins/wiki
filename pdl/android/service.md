# Service

## Template

## 執行模式

Service 有四種執行模式，在 `StartCommand()` 的回傳值裡可以設定：

```java
public class MyService extends Service {
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {

        return START_STICKY;
    }
}
```

四種執行模式說明如下：

* **START_STICKY** Service 強制結束後會重啟，但是不保留 Intent
* **START_NOT_STICKY** Service 強制結束後，不會重啟
* **START_REDELIVER_INTENT** Service 強制結束後會重啟，也會保留 Intent
* **START_STICKY_COMPATIBILITY** START_STICKY 的兼容版本，但不一定有效
