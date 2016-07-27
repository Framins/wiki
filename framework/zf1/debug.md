# Debug

最基本的顯示錯誤訊息：在 application.ini 裡加入下面的設定值即可：

```ini
; php 基本錯誤訊息
phpSettings.display_startup_errors = 1
phpSettings.display_errors = 1

; 如果有 exception 的時候，這個要設 1 才會噴錯誤訊息
resources.frontController.throwExceptions = 1
```
