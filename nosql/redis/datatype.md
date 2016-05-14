DataType
========

String
------

String 是最基本的型態。可以使用 SET 給 key 設定一個 string ；使用 GET 取得該 key 所儲存的值。

String 也可以儲存數字，然後就可以使用 INCR 和 DECR 對數字做加減的動作，就有如計數器或計時器一樣。

List
----

List 是很多 String 的集合，它有著一定的順序排列。它的概念就像左右打開的一條鏈 (chain)，可以在左邊 (front) 或右邊 (rear) 追加新元素；也可以加在中間，但會嚴重影響效能。

List 使用 LPUSH 和 RPUSH 追加元素； LPOP 和 RPOP 取得並移除元素； LRANGE 取得一定範圍的元素(不會刪除)； LSET 可以在指定位置設定元素等。

Hash
----

Hash 跟一般程式語言看到的 Hash 資料結構是一樣的 (如 Java 的 HashMap(), Javascript的 Object() ...) 不過這裡的 key 是稱作 field 。

Set
---

Set 是不重複 String 的集合－－如同 Java 的 [Set](http://developer.android.com/reference/java/util/Set.html)－－跟 List 不同的地方在於，它是無序且不能重複； List 是有順序且值可以重複。

可以使用 SADD 為 Set 加新的元素； SREM 移除元素； SPOP 取得並移除元素。也可以作集合操作，如 SUNION - 聯集、 SINTER - 交集、 SDIFF - 差集等動作。

Ordered Set
-----------

Ordered Set 跟 Set 很像，不同的地方在於， Ordered Set 每個元素多了一個權重值 (score)，可以拿來跟其他元素比較或排序。

Ordered Set 使用 ZADD 新增元素， ZREM 移除元素，也有獨有的操作，如 ZINCR 是將權重值+1， ZSCORE 是取得權重值。
