# Lifecycle

## Source Code

* [Source Code](source-code.md)

## Result

會打這個記錄，最主要就是要用在狀態的儲存和恢復，還有旋轉螢幕的功能該如何實作。參考下面文章：

* [Android Screen Orientation Event螢幕方向處理+Acitivity Liftcycle](http://wazai.net/2120/android-screen-orientation-event%E8%9E%A2%E5%B9%95%E6%96%B9%E5%90%91%E8%99%95%E7%90%86acitivity-liftcycle)
* [【亲测】Activity中的 ConfigChanges 属性以及横竖屏切换时候 Activity 的生命周期](http://www.cnblogs.com/charley_yang/archive/2011/04/17/2018940.html)

### 首次執行

|  Class  |  Method  |
|  -----  |  ------  |
| Main | onCreate |
| MainFragment | onAttach |
| Main | onAttachFragment |
| MainFragment | onCreate |
| MainFragment | onCreateView |
| MainFragment | onViewCreated |
| MainFragment | onActivityCreated |
| Main | onStart |
| MainFragment | onStart |
| Main | onPostCreate |
| Main | onResume |
| MainFragment | onResume |
| Main | onPostResume |
| Main | onCreateOptionsMenu |
| Main | onPrepareOptionsMenu |

### Main按Home鍵回到桌面

|  Class  |  Method  |
|  -----  |  ------  |
| MainFragment | onPause |
| Main | onPause |
| Main | onSaveInstanceState |
| MainFragment | onSaveInstanceState |
| MainFragment | onStop |
| Main | onStop |

### 多工鍵返回或按程式重新進入Main

|  Class  |  Method  |
|  -----  |  ------  |
| Main | onRestart |
| Main | onStart |
| MainFragment | onStart |
| Main | onResume |
| MainFragment | onResume |
| Main | onPostResume |

### 多工鍵把程式關閉

無任何訊息

### 把程式關閉後再點程式進入

|  Class  |  Method  |
|  -----  |  ------  |
| Main | onCreate |
| MainFragment | onViewStateRestored |
| MainFragment | onAttach |
| Main | onAttachFragment |
| MainFragment | onCreate |
| MainFragment | onCreateView |
| MainFragment | onViewCreated |
| MainFragment | onActivityCreated |
| Main | onStart |
| MainFragment | onStart |
| Main | onPostCreate |
| Main | onResume |
| MainFragment | onResume |
| Main | onPostResume |
| Main | onCreateOptionsMenu |
| Main | onPrepareOptionsMenu |

> 第2個 MainFragment.onViewStateRestored() ，有 API Level 17 的限制。


### Main執行finish或按返回鍵

這兩個動作的結果是一樣的。

|  Class  |  Method  |
|  -----  |  ------  |
| MainFragment | onPause |
| Main | onPause |
| MainFragment | onStop |
| Main | onStop |
| MainFragment | onDestroyView |
| MainFragment | onDestroy |
| MainFragment | onDetach |
| Main | onDestroy |

### Main 切換到 Sub

不管有沒有要回傳，都會是以下的結果。

|  Class  |  Method  |
|  -----  |  ------  |
| MainFragment | onPause |
| Main | onPause |
| Sub | onCreate |
| SubFragment | onAttach |
| Sub | onAttachFragment |
| SubFragment | onCreate |
| SubFragment | onViewCreated |
| SubFragment | onActivityCreated |
| Sub | onStart |
| SubFragment | onStart |
| Sub | onPostCreate |
| Sub | onResume |
| SubFragment | onResume |
| Sub | onPostResume |
| Sub | onCreateOptionsMenu |
| Sub | onPrepareOptionsMenu |
| Main | onSaveInstanceState |
| MainFragment | onSaveInstanceState |
| MainFragment | onStop |
| Main | onStop |

### Sub 執行 finish

包括有回傳值的也是一樣的結果

|  Class  |  Method  |
|  -----  |  ------  |
| SubFragment | onPause |
| Sub | onPause |
| MainFragment | onActivityResult, requestCode: 10 , resultCode: 10 |
| Main | onRestart |
| Main | onStart |
| MainFragment | onStart |
| Main | onResume |
| MainFragment | onResume |
| Main | onPostResume |
| SubFragment | onStop |
| Sub | onStop |
| SubFragment | onDestroyView |
| SubFragment | onDestroy |
| SubFragment | onDetach |
| Sub | onDestroy |

### Main 翻轉螢幕

|  Class  |  Method  |
|  -----  |  ------  |
| MainFragment | onPause |
| Main | onPause |
| Main | onSaveInstanceState |
| MainFragment | onSaveInstanceState |
| MainFragment | onStop |
| Main | onStop |
| MainFragment | onDestroyView |
| MainFragment | onDestroy |
| MainFragment | onDetach |
| Main | onDestroy |
| Main | onCreate |
| MainFragment | onAttach |
| Main | onAttachFragment |
| MainFragment | onCreate |
| MainFragment | onCreateView |
| MainFragment | onViewCreated |
| MainFragment | onActivityCreated |
| Main | onStart |
| MainFragment | onStart |
| Main | onRestoreInstanceState |
| Main | onCreateOptionsMenu |
| Main | onPrepareOptionsMenu |
| Main | onPostCreate |
| Main | onResume |
| MainFragment | onResume |
| Main | onPostResume |

### 加入 android:configChanges 設定後， Main 翻轉螢幕

在 `AudroidManifest.xml` 加入 android:configChanges 設定：

* android:configChanges="orientation"
* android:configChanges="orientation|screenSize" (API level 13以上)
* android:configChanges="orientation|keyboardHidden" (使用 AVD 模擬器測試)

|  Class  |  Method  |
|  -----  |  ------  |
| Main | onConfigurationChanged |
| MainFragment | onConfigurationChanged |

剛剛翻轉螢幕的動作全不見了，只剩下 onConfigurationChanged 。
