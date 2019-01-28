# AndroidManifest.xml

這裡有很多Android App整體相關的設定

## activity

父元素：

* application

子元系：

* intent-filter
* meta-data

### android:configChanges

[官方說明](http://developer.android.com/guide/topics/manifest/activity-element.html#config)

在 configuration 的某些屬性發生變化的時候， Activity 會關閉並重新啟動。但如果當這裡有設定某些 configuration 相關的屬性值，則當該屬性值發生變化的時候， Activity 就不會重啟，而會換成呼叫[onConfigurationChanged()](http://developer.android.com/reference/android/app/Activity.html#onConfigurationChanged(android.content.res.Configuration))。

|  Value  |  Description  |
|  -----  |  -----------  |
| mcc | 移動國家代碼, 由三位數字組成。每個國家都有自己獨立的 MCC ，可以用來識別手機用戶所屬的國家 |
| mnc | 移動網路訊號，用來區分手機用戶所使用的電信業者 |
| locale | 語系改變 |
| touchscreen | |
| keyboard | 鍵盤模式發生變化，如接入外部鍵盤 |
| keyboardHidden | 打開手機內建鍵盤 |
| navigation | |
| screenLayout | 螢幕佈局改變 |
| fontScale | 字型大小改變 |
| uiMode | UI模式改變， API level 8 新增 |
| orientation | 方向改變。如果使用 API level 13 以上時，那還需要另外加 screenSize ，因為螢幕大小的確也發生變化 |
| screenSize | 螢幕大小改變， API level 13 新增 |
| smallestScreenSize | API level 13 新增 |
| layoutDirection | Layout 方向改變， API level 17 新增 |

可以用在不想重新啟動 Activity 的情況下，如：

螢幕方向改變

```
android:configChanges="orientation|keyboardHidden"
// API level 13 or high
android:configChanges="orientation|keyboardHidden|screenSize"
```

### android:screenOrientation

[官方說明](http://developer.android.com/guide/topics/manifest/activity-element.html#screen)

此設定會決定螢幕的方向為何，此設定要使用的常數值如下：

|  Value  |  Description  |  API Level  |
|  -----  |  -----------  |  ---------  |
| unspecified | 預設值，由系統自己選方向，不同的設備會有不同的結果 | 1 |
| behind | Acitivty 前一個 Activity 相同的方向 | 1 |
| landscape | Landscape 方向，寬度比高度大 | 1 |
| portrait | Portrait 方向，高度比寬度大 | 1 |
| reverseLandscape | Landscape 的反方向 | 9 |
| reversePortrait | Portrait的 反方向 | 9 |
| sensorLandscape | 可以是 Landscape 或 reverseLandscape ，依感應器的方向決定 | 9 |
| sensorPortrait | 可以是 Portrait 或 reversePortrait ，依感應器的方向決定 | 9 |
| userLandscape | | 18 |
| userPortrait | | 18 |
| sensor | 依使用者的方向感應器決定螢幕方向，可以使用的方向為系統決定。 | 1 |
| fullSensor | sensor 有的方向系統是不允許的，使用這個就是四個方向全都可以使用 | 9 |
| nosensor | sensor 的功能會被忽視，其他跟 unspecified 一樣 | 1 |
| user | 使用 user 目前首選的方向 | 1 |
| fullUser | | 18 |
| locked | | 18 |

### android:windowSoftInputMode

[官方說明](http://developer.android.com/guide/topics/manifest/activity-element.html#wsoft)

這個設定決定了 Activity 與 SoftInput 的互動會是如何。

它會影響兩件事

* SoftInput 的狀態。當 Activity 處於 focus 時，決定它是否顯示。
* ActivityWindows 的調整。是否要減少 ActivityWindows 大小以便騰出空間放 SoftInput ；是否當使用中視窗的部分被 softInput 覆蓋時它的內容的當前焦點是可見的。

它能設的是常數字串，也可以多組組合：

|  Value  |  Description  |
|  -----  |  -----------  |
| stateUnspecified | SoftInput 不指定狀態，系統會自動選擇。這也是預設值。 |
| stateUnchanged | |
| stateHidden | |
| stateAlwaysHidden | |
| stateVisible | |
| stateAlwaysVisible | |
| adjustUnspecified | 不指定視窗調整的方法。 |
| adjustResize | 指定視窗要調整大小。 |
| adjustPan | 指定視窗不調整大小。 |
