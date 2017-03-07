# Zend_Session

* [官方教學文件](http://framework.zend.com/manual/1.12/en/zend.session.html)
* [API 文件](http://framework.zend.com/apidoc/1.12/files/Session.html)

使用注意：

* 不要執行 `session_start()`
* php.ini 要關閉 session.auto_start (session.auto_start 0)
* 因為 Session 是全域，所以使用時需要注意重複命名的問題，可以使用 `Zend_Session_Namespace`

# Zend_Session_Namespace

* [API文件](http://framework.zend.com/apidoc/1.12/files/Session.Namespace.html)

提供具備命名空間的 session 功能
