# Database

Android 內建 SQLite 函式庫。建資料庫必需要依照 Android 的版本控制規則去寫 Class，當資料庫建立完成後，實際操作就跟一般使用 SQLite 差不多了。

## Third-Party Library

資料庫操作也漸漸由寫 SQL 語法轉變為物件寫法，所以也可以考慮使用 [ORM](http://zh.wikipedia.org/wiki/ORM) 函式庫。

* [GreenDao](http://greendao-orm.com/) - 應該是速度最快的，使用起來也最麻煩的。
* [ORMLite](http://ormlite.com/) - 使用 Annotation 和 Reflection 去存取 ORM Class 的資料。
* [ActiveAndroid](https://github.com/pardom/ActiveAndroid)
* [Sprinkles](https://github.com/emilsjolander/sprinkles)
* [SQLiteDAO](https://code.google.com/p/android-sqlite-dao/) - 同 ORMLite。
* [AFinal](http://www.afinal.org/) - 功能很強，但說明文件太少，需要自己去翻原始碼。

## References

* [android.database.sqlite](http://developer.android.com/reference/android/database/sqlite/SQLiteDatabase.html)
* [Saving Data in SQL Databases](http://developer.android.com/training/basics/data-storage/databases.html)
