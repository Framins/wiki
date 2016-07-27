# Selector

  * [W3C 定義的 Selector ](http://www.w3.org/TR/css3-selectors/#selectors)
  * http://www.w3school.com.cn/cssref/css_selectors.asp
  * [Fraina 整理的](http://fraina.distract.org/stm/doku.php?id=front-end:css3#selector)
  * [CSS Diner](http://flukeout.github.io/) - 玩遊戲學 CSS
  * [The 30 css selectors you must memorize](http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)
  * [jQuery Tutorial & Examples](http://hmkcode.com/jquery-tutorial/) - CSS Selector 的大表哥 jQuery Selector。

## List of Selector

|  Version  |  Selector  |  Example  |  Description  |  Remark  |
|  -------  |  --------  |  -------  |  -----------  |  ------  |
|  1  | .class | `.className` | `class="className"` 屬性的元素 | |
|  1  | #id | `#idName` | `id="idName"` 屬性的元素 | |
|  2  | * | `*` | 所有元素 | |
|  1  | element | `p` | 所有 `<p>` 元素 | |
|  1  | element, element | `div, p` | 所有 `<div>` 元素和所有 `<p>` 元素 | |
|  1  | element element | `div p` | `<div>` 元素內部所有 `<p>` 元素 | |
|  2  | element>element | `div>p` | 父元素為 `<div>` 元素的所有 `<p>` 元素 | |
|  2  | element+element | `div+p` | 在相同的父元素下，緊臨在 `<div>` 元素之後的 `<p>` 元素 | |
|  2  | [attribute] | `[type]` | 帶有 `type` 屬性的所有元素 | |
|  2  | [attribute=value] | `[type=password]` | `type="password"` 屬性的所有元素 | |
|  2  | [attribute~=value] | `[title~=word]` | `title` 屬性，包含單字 `word` 的所有元素 | |
|  2  | %%[attribute|=value]%% | `[title|=word]` | `title` 屬性，以單字 `word` 開頭的所有元素 | |
|  1  | :link | `a:link` | 所有未被點擊過的連結 | 只適用於`<a>` |
|  1  | :visited | `a:visited` | 所有已被點擊過的連結 | 只適用於`<a>` |
|  1  | :active | `div:active` | 被點擊的元素 | 有點像 `onClick` 事件 |
|  1  | :hover | `span:hover` | 被滑過的元素 | 有點像 `onHover` 事件 |
|  2  | :focus | `input:focus` | 取得焦點的元素 | 有點像 `onFocus` 事件 |
|  1  | :first-letter | `p:first-letter` | `<p>` 元素的首字 | |
|  1  | :first-line | `p:first-line` | `<p>` 元素的首行 | |
|  2  | :first-child | `p:first-child` | `<p>` 元素的首行 | |
|  2  | :before | `p:before` | 在 `<p>` 元素的內容之前插入新的內容 | 使用 `content` 屬性設定文字內容 |
|  2  | :after | `p:after` | 在 `<p>` 元素的內容之後插入新的內容 | 使用 `content` 屬性設定文字內容 |
|  2  | :lang(language) | `p:lang(en)` | `lang` 屬性為 `en` 開頭的 `<p>` 元素 | |
|  3  | element1~element2 | `p~ul` | 在相同的父元素下， `<p>` 之後的所有 `<ul>` 元素 | |
|  3  | %%[attribute^=value]%% | `%%a[src^="https"]%%` | `<a>` 元素的 `src` 屬性，以 `https` 開頭 | |
|  3  | %%[attribute$=value]%% | `%%a[src$=".pdf"]%%` | `<a>` 元素的 `src` 屬性，以 `.pdf` 結尾 | |
|  3  | %%[attribute*=value]%% | `%%a[src*="abc"]%%` | `<a>` 元素的 `src` 屬性，包含子字串 `abc` | |
|  3  | :first-of-type | `p:first-of-type` | 在相同的父元素下，第一個 `<p>` 元素 | |
|  3  | :last-of-type | `p:last-of-type` | 在相同的父元素下，最後一個 `<p>` 元素 | |
|  3  | :only-of-type | `p:only-of-type` | 在相同的父元素下，唯一一個 `<p>` 元素 | |
|  3  | :only-child | `p:only-child` | 在相同的父元素下，唯一的子元素 `<p>` | |
|  3  | :nth-child(n) | `p:nth-child(n)` | 在相同的父元素下，第 n 個子元素 `<p>` | n |
|  3  | :nth-last-child(n) | `p:nth-last-child(n)` | 在相同的父元素下，倒數第 n 個子元素 `<p>` | n |
|  3  | :nth-of-type(n) | `p:nth-of-type(n)` | 在相同的父元素下，第 n 個 `<p>` 元素 | n |
|  3  | :nth-last-of-type(n) | `p:nth-last-of-type(n)` | 在相同的父元素下，倒數第 n 一個 `<p>` 元素 | n |
|  3  | :last-child | `p:last-child` | 在相同的父元素下，最後一個子元素 `<p>` | |
|  3  | :root | `:root` | DOM 的根元素 | |
|  3  | :empty | `p:empty` | 沒有子元素的 `<p>` 元素 | |
|  3  | :target | `#news:target` | 當前被選擇的錨點 `#news` 元素 | |
|  3  | :enabled | `input:enabled` | 每個被啟用的 `<input>` 元素 | |
|  3  | :disabled | `input:disabled` | 每個被禁用的 `<input>` 元素 | |
|  3  | :checked | `input:checked` | 每個被選取的 `<input>` 元素 | |
|  3  | :not(selector) | `:not(p)` | `<p>` 以外的所有元素 | |
|  3  | ::selection | `::selection` | | |

## Class Selector

Class選擇器， `.` 開頭，後面接 class 屬性的名稱，[名稱命名方法參考](http://www.regexper.com/#%5Ba-zA-Z_%5D%5B0-9a-zA-Z-_%5D*%7C%5B-%5D%5Ba-zA-Z_%5D%5B0-9a-zA-Z-_%5D*)

一個網頁可以有多個 class 屬性，如：

```html
<p class="tip">段落一</p>
<p class="tip">段落二</p>
<p class="notice">段落三</p>
```

程式碼如下：

```css
.tip { color: blue; } /* 段落一二會是藍色 */
.notice { color: red; } /* 段落三會是紅色 */
```

## ID Selector

`#` 開頭，後面接 id 屬性的名稱，[名稱命名方法參考](http://www.regexper.com/#%5Ba-zA-Z_%5D%5B0-9a-zA-Z-_%5D*%7C%5B-%5D%5Ba-zA-Z_%5D%5B0-9a-zA-Z-_%5D*) (同 class selector)

**一個網頁只能有一個 id 屬性**，如：

```html
<p id="tip">段落一</p>
<p id="notice">段落二</p>
```

程式碼如下：

```css
#tip { color: blue; } /* 段落一會是藍色 */
#notice { color: red; } /* 段落二會是紅色 */
```

## Type Selector

型態選擇器，是直接設定在 html 標籤上。

```css
h1 { color: blue; } /* 所有 h1 標籤會是藍色 */
p { color: red; } /* 所有 p 標籤會是紅色 */
```

## Universal Selector

通用選擇器，使用萬用字元 `*` ，所有元素都會套用設定。

```css
* { color: red; } /* 所有元素都會被設定紅色 */
```

## Groups of Selectors

選擇器群組，參考以下程式碼：

```css
h1 { color: red; }
h2 { color: red; }
h3 { color: red; }
```

它與下面相等價：

```css
h1, h2, h3 { color: red; }
```

> **注意:** 要全部選擇器都是合法的選擇器，等價才會成立；只要其中有一個選擇器不合法，則全部都會失效。
