# Android Test

常用的 test class

|  Name  |  Description  |
|  ----  |  -----------  |
| AndroidTestCase | 可以用來測試 Android 程式，並使用程式的資源 |
| ActivityUnitTestCase<T extends Activity> | 用來測試 Android 程式中的 Activity 類別，由於是採用「獨立」的單元測試，有些 Activity 的功能無法使用 |
| ActivityInstrumentationTestCase2<T extends Activity> | 用來測試 Android 程式中的 Activity 類別，它不是使用「獨立」的單元測試，因此可以完整地測試 Activity 的功能 |
| ApplicationTestCase<T extends Application> | 用來測試 Application 類別 |
| ProviderTestCase2<T extends ContentProvider> | 用來測試 ContentProvider 類別 |
| ServiceTestCase<T extends Service> | 用來測試 Service 類別 |

## References

* http://developer.android.com/tools/testing/testing_android.html
* http://developer.android.com/tools/testing/activity_testing.html
* http://rritw.com/a/kaifaguanli/danyuanceshi/20121004/233984.html
* http://140.127.82.166/retrieve/18991/91.pdf
