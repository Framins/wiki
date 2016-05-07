HTML
====

標籤參考：

* [HTML各版本與支援的標籤](http://w3c.github.io/elements-of-html/)
* [HTML 5.1 (未定案)](http://www.w3.org/TR/html51/)
* [HTML 4 & 5 教學](http://www.w3schools.com/html/default.asp)

Coding Style 參考：

* [程式碼準則 by @mdo](http://lisp.es/code-guide/#html)

Tag
---

標籤參考：

* https://developer.mozilla.org/en-US/docs/Web/HTML/Element
* http://www.w3schools.com/html/html5_new_elements.asp
* [HTML5 inputs and attribute support](https://www.miketaylr.com/code/input-type-attr.html) 

語意標籤
--------

* [Semanitc Elements](http://www.w3schools.com/html/html5_semantic_elements.asp)
* [HTML5的語意標籤與文件結構](http://www.dotblogs.com.tw/yuan0716/archive/2011/11/10/html5newtag.aspx)
* [Introducing HTML5 footer, header, nav, article, section and aside elements](http://www.cellbiol.com/bioinformatics_web_development/doku.php/chapter_3_-_your_first_webpage_-_learning_html_and_css/introducing_html5_footer_header_nav_article_section_aside_elements)
* [HTML5標記div、section、article使用說明](http://yongxjb.pixnet.net/blog/post/6312952-html5%E6%A8%99%E8%A8%98div%E3%80%81section%E3%80%81article%E4%BD%BF%E7%94%A8%E8%AA%AA%E6%98%8E_19)

|  Tag  |  Description  |  Reference  |
|  ---  |  -----------  |  ---------  |
| header | 網頁的頂部，網頁最重要形象和資訊都會放在這裡，如 logo、網站名詞等。 | [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header) |
| nav | 網站的導航連結或選單 | [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/nav) |
| aside | 直譯是「旁白」，表示文章以外的內容，通常用在文章內容側欄 |  |
| article | 網頁可以有很多文章(如 blog )，這時可以用 article 區分文章內容 | [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) |
| section | 文章內的章節或小段落((即 section 會放在 article 裡))，通常會有一個 heading ((h1~h6 tag))  | [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) |
| footer | 網頁的底部，通常是作者相關資訊，如著作權、作者名、使用什麼引擎等。 | [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer) |

用語音標籤的好處是，看標籤就知道該內容應該會是什麼功能，在查看和維護會變得更容易。

另外在 SEO 也是會有幫助的

* [How To Use H1-H6 HTML Elements Properly](http://www.hobo-web.co.uk/headers/)

### `<dl><dt><dd>`

* [HTML dl dt dd 標籤](http://www.wibibi.com/info.php?tid=353)

通常用在定義或是名詞解釋等。

* *dl* Definition List，清單 
* *dt* Definition Term，項目
* *dd* Definition Description，描述

一個 dl 裡面，會有很多組 dt + dd，dt + dd 是一組一組的搭配，dd 會自動產生縮排的效果。

與 li 不同的是，它預設 dd 就會自動縮排，而 li 需要再包一層 ul 才行。所以單純的項目列表還是用 li 會比較明確，而一個主項目和一個單行描述的組合，用 dl 會比較合適。

### `<label>`

設定 form 元件的標示，可用文字或圖片。一個標示可以指定一個 input ，當 user 點擊 label 的時候，就等同點擊 input 。

Attributes:

<label> 支援 Global Attributes, Event Attributes

|  Attribute  |  Value  |  Description  |  Example  |  Remark  |
|  ---------  |  -----  |  -----------  |  -------  |  ------  |
| for | input id | 設定該 label 所指定的 input | `<lable for="text">Text</lable>` | |
| form | form id | 設定指定的 form id ，有多個的話可以用空格分隔 |  | HTML5 新增 |

### `<a>`

無作用連結的做法：

```html
<a href="javascript: void(0)">連結</a> 
```

另解

```html
<a href="#">連結</a> 
```

[參考](http://blog.xuite.net/vexed/tech/25193980-%E7%84%A1%E4%BD%9C%E7%94%A8%E9%80%A3%E7%B5%90%E8%A9%B2%E5%AF%AB+%3Ca+href%3D%22%23%22+%3E+%E9%82%84%E6%98%AF+%3Ca+href%3D%22javascript%3A+void(0)%22+%3E)
