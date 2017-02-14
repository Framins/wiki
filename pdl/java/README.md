Java
====

歷史和用途，直接網路比較快。

Basic
-----

* [final](final.md)

Standard class library
----------------------

java.lang ，基本核心類，包括字串，執行緒、例外和反射等。

* java.lang.object - Java 所有定義物件的最上層的 Class，又稱 [[http://docs.oracle.com/javase/tutorial/java/IandI/objectclass.html|SuperClass]]
  + java.lang.string - 字串物件，這應該也是最常用的物件

java.util ，輔助工具類，包括常用的雜湊、串列、集合等。

* java.util.collection - 所有集合種類的 SuperClass
* java.util.list - 循序有索引的串列
* java.util.set - 不允許重複相同物件的集合
* java.util.map - 「鍵-值」（Key-Value）存取的 Map

Commonly used but often FORGET
------------------------------

常用又常忘的東西

### Array and ListArray transform

List 轉 Array，使用的是 List 的 public 方法 `toArray()`

```java
List<String> list;

String[] array = list.toArray(new String[0]);
```

Array 轉 List，使用的是 Arrays 的靜態方法 `asList()``

```java
import java.util.Arrays;

String[] array;

List<String> list= Arrays.asList(array);
```
