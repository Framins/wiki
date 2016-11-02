CAP Theorem
===========

CAP 定理，或稱為布魯爾定理 *Brewer's theorem* ，它指出對於一個分散式計算系統來說，不可能同時滿足以下三點

* **Consistency:** 一致性 (所有節點在同一時間具有相同的數據)
* **Availability:** 可用性 (保證每個請求不管成功或者失敗都有響應)
* **Partition tolerance:** 分區容錯性 (系統中任意信息的丟失或失敗不會影響系統的繼續運作)

根據定理只能滿足兩項，不可能同時滿足三項。

> 大部分的問題都會是在寫，而不是在讀，因此 CAP 其實是在講寫的問題。

References
----------

* [CAP定理](https://zh.wikipedia.org/wiki/CAP%E5%AE%9A%E7%90%86)
* [NoSQL學習筆記(二)之CAP理論](http://myblog-maurice.blogspot.tw/2012/08/nosqlcap.html)
* [CAP理論十二年回顧："規則"變了](http://myblog-maurice.blogspot.tw/2012/08/cap_21.html)
* [分布式系統理論基礎 - CAP](https://read01.com/y2x0nB.html)
