# Sensor

Android 官方是把 Sensor 和 Location 放在 [Location and Sensors API](http://developer.android.com/guide/topics/sensors/index.html) 中。但程式上，它們是不同的 Manager 。合理來說， GPS 也是一種感應器，所以都放在 Sensor 分類也並沒有什麼錯囉。

## Location

官方有 Location 的教學: [Making Your App Location-Aware](http://developer.android.com/training/location/index.html)

### Required Permission

Location 相關的權限

| Name | Description |
| ---- | ----------- |
| android.permission.ACCESS_COARSE_LOCATION | 允許從 CellID 或 WiFi 熱點來取得粗略的位置 |
| android.permission.ACCESS_FINE_LOCATION | 允許從 GPS 取得精確位置 |
| android.permission.ACCESS_LOCATION_EXTRA_COMMANDS | 允許應用程式存取額外的位置相關指令 |
