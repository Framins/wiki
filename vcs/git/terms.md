# Glossary of terms

名詞間的關聯也一併解釋。

## repository

簡稱 *repo*，中譯檔案庫，裡面記錄了所有變動的歷史，可供追縱或回朔。

## log

## branch

分支，如同樹的分支一樣，都源自同一個根的養分，但長出來的姿態都不一樣。

## change

參考官方教學文： http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository

因此可以得知，change 可以包括下列行為：

* git add
* git rm
* git mv

change 相關的名詞：

* change 後，需要做 commit，才會在記錄在 local repository 裡供查詢。

## commit

中譯為提交。每一次的提交都是 repo 歷史上的一個節點，這也是可以追縱或回朔的參考點。

* commit 即為 log 裡面的每一個節點
* 一個 commit 包含一個以上的 change
* merge 也是一種 commit

commit 都可以隨意修改、複製、移動、拆分、合併，但是要記得 git 做這些事的原則全都是新增，而不會真的做修改或刪除。

## remote

中譯為遠端。Git 是分散管理，所以一定會有本機的 repo，有本機當然會有遠端。

遠端的 repo 一樣會有 branch 可以切換或管理等。

## clone

clone 沒有比較好的中文翻譯，大概就像 duplicate 這種比較完整的複製。
clone 會把 remote 整個 repository 都下載到本機，包括 log 的 commit 和相關檔案等。
同時也會把 remote 的資訊記錄起來，方便未來要做 push 和 pull。

## push

push 可以把本機的 branch 上傳到 remote 上。
為考量安全，push 預設是不能覆蓋舊有 branch 的歷史 commit。必須要是舊有 branch 之後的 commit 才行。

## fetch

fetch 做的事跟 clone 差不多，會把 remote repo的資訊下載回來到本機，並把 remote branch 位置都設定在正確的位置。

本機可以切換到 remote 新完成的 branch 來做測試或檢視的動作。

## merge

合併，merge 可以把兩個 commit 做合併，過程中程式會自動做合併，並做記錄。如果有遇到程式無法自動合併的，則會顯示 conflict，要換由手動修正才能做 merge。

merge 會建立一個新的 commit，然後把上述的過程，記錄在這個 commit 裡。所以 merge 是能 reset 的。

## pull

pull 簡單來說，就是把 remote 的資料 fetch 下後再 merge，兩個動作合在一起。

## reset

重置，說重置並不是表示它只能往以前走，只要有 commit，它都能用 reset 到那個 commit 上，當然常用的還是還原到前一個 commit 做處理。

需要注意的是，它有三種不一樣的參數：

* *mixed* 會把你做過的修改仍然保留
* *soft* 會把做過的修改加入 stage
* *hard* 把做過的修改完全刪除，回到那個版本原本的樣子。

## rebase

rebase，英文字面上就是重新定義基礎。大概就像接枝一樣，把某個 branch 剪下來後，接到另一個 branch 上。

rebase 除此之外還可以用在 push 之前的整理 commit，commit 的重點是在要讓成員好懂。但通常一開始的 commit 都很寫的很爛，因此可以靠這個 rebase 來做到重新整理 commit，讓其他開發者都能了解。

## tag

標籤，通常都是標上版本號，讓開發者可以有個依據去找到該版本號的原始碼等。
