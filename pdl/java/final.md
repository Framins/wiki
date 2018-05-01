# final

final 在 Java 程式中出現的位置有很多地方，但是代表的意思也有點不大一樣，因此才出現了這個筆記。

## Modify Member

定義類別的基本型態成員時，可以加上 final 關鍵字。

```java
public class Circle {
    final double PI = 3.14;
}
```

表示這個成員在定義的時候就決定了它的值，之後都不能更改，就像 PHP 的常數一樣 (const)。相對的， final 常數要在一開始就指定一個靜態的值。

## Modify Object Member

```java
public class Circle {
    final ArrayList<Integer> points;
}
```

概念與基本型態大同小異，不一樣的地方是它可以在Constructor裡初始化。\\
而因為物件存的都是reference，所以它不能更改的部分只是reference，物件裡面的成員依然可以更改。

## Modify Method

final 加在 method 上時，代表這個 method 不能再被 override 了，但是還是能被 overload 。

```java
public class Circle {
    public final int getX() {};
}
```
