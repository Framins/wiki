# Set

Set 是指數學名詞「集合」。集合基本的定義就是「一堆東西」，這些「東西」稱作元素。

集合的特性：

* 無序性：裡面的每個元素的權重皆相同
* 互異性：裡面的元素不會重複
* 確定性：假設有一個集合和一個元素，這個元素要嘛就是在集合裡，要嘛就是不在集合裡，不該有模稜兩可的情況發生

> PS1: 可以在集合上定義序關係，有了序關係，元素間就會照序關係排列。但集合本身的特性而言，元素間本來就沒有順序性了  
> PS2: 如果需要讓一個元素在集合內出現多次，可以使用 [多重集](http://zh.wikipedia.org/wiki/%E5%A4%9A%E9%87%8D%E9%9B%86)

集合的名詞：

* 空集(∅，empty set) - 沒有任何元素的集合
* 子集(⊆，subset) - A ⊆ B，A 所有元素皆屬於 B
* 父集(⊇，superset) - A ⊇ B，B 所有元素皆屬於 A
* 聯集(∪，union) - A ∪ B，所有 A 和 B 的元素，而沒有其他元素的集合
* 交集(∩，intersection) - A ∩ B，所有同時屬於 A 和 B 的元素的集合
* 差集(\，complement) - A \ B，所有屬於 A 但不屬於 B 的元素的集合
* 互斥集(disjoint sets) - A 和 B 集合沒有交集

## Example

* Miles 在玩的音 Game ： {jubeat, IIDX, GITADORA, DEA}
* Fraina 在玩的音 Game ： {jubeat, DEA}

可導出以下結果：

1. Fraina 是 Miles 的子集 ( Fraina ⊆ Miles)，表示 Fraina 在玩的音 Game，Miles 都有在玩。
2. 在兩個人聯集 (Fraina ∪ Miles)的集合： {jubeat, IIDX, GITADORA, DEA}，會看到其中一個人（或兩個人一起）在玩音 Game。
3. 在兩個人交集 (Fraina ∩ Miles)的集合： {jubeat, DEA}，會看到兩個人一起玩音 Game，這是兩個人共同的交集。
4. Miles 有玩但 Fraina 不玩的音 Game 集合 {IIDX, GITADORA}，是差集 Miles \ Fraina 的集合；反之，Fraina 有玩但 Miles 不玩的音 Game 集合 {}，是差集 Fraina \ Miles 的集合。

## Sequential Container

達成一個 Set 最簡單的方法：開一個 Array 再放入個別的元素，只要確保元素不重複即可。相同的道理，[Linked List](linked-list)，Tree 也都能實作出 Set只是這種資料結構做聯集、交集、差集之類的運算，會比較麻煩，也比較慢。

## Associative Container

另一種表達方法，是用對應的方式。比方說有個 Array[10]。如果這集合裡有 3 這個資料，則讓 Array[3] 是 true。

這個資料結構的缺點是有大小的限制，受 Array 大小直接影響，但好處是在做聯集、交集、差集之類的運算，就顯得簡單並快速許多。

## Hash Table

## Implement

程式實作

### PHP

對 Array 的處理，PHP 有預設 function 可以使用：

  * 交集：[array_intersection()](http://tw1.php.net/manual/en/function.array-intersect.php)
  * 差集：[array_diff()](http://tw1.php.net/manual/en/function.array-diff.php)
  * 聯集：沒有內建，不過可以先用 [array_merge()](http://tw1.php.net/manual/en/function.array-merge.php) 合併後，再用 [array_unique()](http://tw1.php.net/manual/en/function.array-unique.php) 把重複的元素去除，如：

```php
function array_union($a, $b) {
    $union = array_merge($a, $b);
    $union = array_unique($union);
    return $union;
}
```

## References

* [Set](http://www.csie.ntnu.edu.tw/~u91029/Set.html)
* [集合的運算](http://ocw.nctu.edu.tw/upload/classbfs1210110227144219.pdf)
* [集合](http://user.frdm.info/ckhung/b/dm/set.php)
* [Hash 和 Bloom Filter](http://www.sigma.me/2011/09/13/hash-and-bloom-filter.html)
* [MMDays專欄](http://mmdays.com/2007/12/25/set_manifolds/) | 集合: 從邏輯到1+1=2
