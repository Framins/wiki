# Hook

http://git-scm.com/book/zh-tw/v1/Git-%E5%AE%A2%E8%A3%BD%E5%8C%96-Git-Hooks

hook 有分 client 端和 server 端

在專案目錄下的 `.git/hooks/` 裡，就有各個 hook 的範例可以參考了

## pre-commit

在 commit 之前會先執行做某些動作，甚至可以經由這些動作的結果來決定這次 commit 能不能成功.

常見做法：

* 把程式碼先做過 Formatting 後，再 commit。
* 先做 unit test 或 coding style 檢查，當通過才能 commit。

### Examples

* [Git Hook in PHP](/pdl/php/tricks.md)
* [先做 JSlint 再 commit 例子](http://rettamkrad.blogspot.tw/2014/03/git-hook-how-to-use-git-pre-commit-hook.html)

## post-checkout

這會在 checkout 成功後執行

常見做法：

* 某些資源同時有下列情況：可由原始碼產生、專案需要用的資源，通常這些資源也都不希望被加入 repo，這時可以用 `post-checkout` 自動執行。如 SCSS -> CSS

## Reference

* https://github.com/wecodemore/grunt-githooks
