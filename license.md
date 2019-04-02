# License

Open source 裡的 code 到底怎樣用才是合法的？

寫了新的 code 要公開原始碼，那要怎麼用才可以保障這個原始碼是不被別人濫用？

## Conclusion

直接從結論開始吧！細節去 google 找即可

簡單來說，以用別人的開源為情境：

* MIT 是最不受限的
* BSD 只受限改作者的名字要原作同意
* Apache 是受限專利權 (詳情要看原文)
* LGPL 是 GPL 的較少限制版
* GPL 限東限西的，使用它（程式上的使用）的程式，就必須要用 GPL 授權

總體來說，可以參考此張圖：

![](https://www.dwheeler.com/essays/floss-license-slide-image.png)

> 圖片來源： [dwheeler.com](https://www.dwheeler.com/essays/floss-license-slide.html)

A -> B，這表示如果同時用到這兩個授權的話，要以 B 為主。換言之，使用 A 開源授權程式的時候，可以用 A 或 B 的授權釋出；相反地，如果使用 B 開源授權程式的話，則不能用 A 授權釋出。

## References

* https://www.hi-linux.com/posts/45101.html
* [如何选择和使用开源许可协议](http://eleveneat.com/2015/12/15/License/)
* [五種開源授權規範的比較 (BSD, Apache, GPL, LGPL, MIT)](http://inspiregate.com/internet/trends/74-comparison-of-five-kinds-of-standard-open-source-license-bsd-apache-gpl-lgpl-mit.html)
