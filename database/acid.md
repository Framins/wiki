ACID
====

在資料庫管理系統裡，為保證 transaction 是正確可靠的，所具備的四個特性：

* Atomicity 原子性
* Consistency 一致性
* Isolation 隔離性
* Durability 持久性

Atomicity
---------

一個事務（transaction）中的所有操作，要麼全部完成，要麼全部不完成，不會結束在中間某個環節。事務在執行過程中發生錯誤，會被回滾（Rollback）到事務開始前的狀態，就像這個事務從來沒有執行過一樣。

Consistency
-----------

在事務開始之前和事務結束以後，資料庫的完整性沒有被破壞。這表示寫入的資料必須完全符合所有的預設規則，這包含資料的精確度、串聯性以及後續資料庫可以自發性地完成預定的工作。

Isolation
---------

當兩個或者多個事務並發訪問（此處訪問指查詢和修改的操作）資料庫的同一數據時所表現出的相互關係。事務隔離分為不同級別，包括讀未提交（Read uncommitted）、讀提交（read committed）、可重複讀（repeatable read）和串行化（Serializable）。

Durability
----------

在事務完成以後，該事務對資料庫所作的更改便持久地保存在資料庫之中，並且是完全的。
