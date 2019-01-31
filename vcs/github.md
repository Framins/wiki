# GitHub

雖然 Git 是個分散式的 VCS，但是 Git 也能做集中管理，但也同時具備了分散管理的特性。所以表示著 repo (repository) 不一定要在 server，也可以在寫程式的人身上。而 [GitHub](https://github.com/) 正是一個做集中管理 repo 的服務。

GitHub 使用上，每個人都可以在上面開 repo，只要有權限，使用者就能 clone 上面看得到 repo，或是 fork 後再 pull request，而且也有 watch repo 和 follow user 等社交網站的功能。當然學程式的朋友們，其實也可以在上面找到很多 public repo，也許會對自己的 project 有用，或是對程式能力有所進步等。

以下內容，會假設看的人已經懂 [Git](git)。

## Sign up

當然免不了的，要先註冊一個帳號才能使用 GitHub 上的服務。帳號有分免費和付費，差別在於免費的 repo 都要 **public**，而付費看付錢的多少來決定 **private** 的多少。

> 容量有聽說是 300MB，但是在付費網頁上並沒找到增加容量的相關資訊。

相對的，就有網站就打著 Unlimited private repo 來吸引 GitHub 使用者。如 [Bitbucket](bitbucket.md)。

**2019 年大更新**

自從 2019 年後，GitHub 調整成一般會員也可以[無限開 private repo](https://blog.github.com/2019-01-07-new-year-new-github/)。不過就以現代常需要多人開發的需求而言，一般會員開 private repo 的條件是蠻嚴苛的，可以參考 [Pricing](https://github.com/pricing) 說明，像 Wiki、Pages、Insights 都不能用在 private repo 上；Code flow 也有限制；最慘的就是 Collaborators 只限定 3 人，比 Bitbucket 還少了一點。

## SSH key

先[產生 SSH Key](/server/ssh/generate-key.md)，接著打開 public key 檔，把內容全部 copy。

GitHub 首頁 → 右上角的頭像 → *Settings* → 左邊 *SSH and GPG keys* → 右邊 *New SSH Key*

Title 是要打一個可以讓你辦別這個 Public Key 是哪一個。Key 是貼上剛剛 copy 的內容，再按 Add key。

這樣就完成了一把 key 與 GitHub 的加密通道了。換言之，換台電腦（含多重開機或虛擬機）以上的動作都可能需要再做一次。

## Create Repository

建立 repo 的方法很簡單，登入後在右上角加號（﹢）裡就有個 *Create a new repo* 可以建立新的 repo。建立新 repo 時，除了 repo name 和 description 之外，會問你要不要用 description 的內容當做是 readme.md 檔來做第一個 commit。這 `README.md` 檔也會是 repo 的首頁介紹內容，只要有修改後再 push，介紹內容也都會依照新 push 的做更新。

另外就是要不要加入參考的 `.gitignore` 檔，針對不同的專案，會有不同的設定。這個設定是參考 [gitignore.io](https://www.gitignore.io/)。建立完後，就會給你一個 HTTPS 或 SSH 的 URI，接著就可以把它當 remote 使用了。

## Clone & Pull & Push

只要有了 URI，想要操作 repo 就不成問題！

比較需要注意的是，因為 repo 都是 public，所以其他 user 都能 clone 和 pull 並不會有什麼問題。
只有 push 的部分一定要有所限制，不然任何路人都能 push 的話，那原始碼的品質就無法保證了不是嗎。
會遇到這個問題，通常都是要協同作業，或是路過的高手好心指導之類的，做法如下：

* 到 repo settings 設定 Collaborators 一起協同作業。這是用在個人 repo 上。
* 建立 organization，並把 repo 綁定在 organization 上，再把成員加入 organization 中。好處是可以在上面建立 ACL，達到 team work。
* 透過 fork / pull request 功能來達成。這是做到 Git 一開始分散處理精神的做法，但一提到分散處理，概念就如同 cache、p2p、parallel computing 一樣，重點在資料一致性了。

## Fork & Pull Request

先提提 collaborator 和 organization 共同處理同個 repo 的缺點：

* 有的 user 可能上班時間做不完想帶回家做，又不想用隨身碟，所以 push 一個暫存的 commit 到 GitHub 是最快的辦法，但變成members都會看到這個無關緊要的 branch。
* 假如 members 夠多、issues 夠多，那 branch 也會非常多。每次 fetch 下來都會看到一堆不是自己要處理 branch，其實也是很煩。但其實這也是 SVN 等集中管理 repo 會遇到的問題。

那回頭來看看當初 VCS 的設計目的，其實就只是－－**歷史記錄回顧**。

來舉最常當例子的**遊戲存檔**，要讀取存檔時，也是要知道那個存檔的詳細資訊。不然讀檔後，發現不是自己要的，又要關掉重來，浪費許多不必要時間。

VCS 也是同個道理，commits 都是未來要看的資訊，也是 reset 的參考點，所以內容都需要是**關鍵且重要**的。

所以上述第一點的做法在 VCS 裡其實並不合理。雖然可以使用 rebase 和 force update 來把暫存的 commit 重新處理過，但別忘了 team work 是要團隊每個成員都要互相配合。

今天有 20 個成員，一旦 push 一個無關緊要的 branch，就會讓其他 19 個成員浪費時間看無關緊要的訊息。

除了靠 user 自己的習慣養成外，其實也可以使用 *fork* 和 *pull request* 來解決。

它其實只是先 clone 到個人的 repo 後，再建立起個人 repo 和 owner repo 間的連結做成的。因為是以 clone 的概念做的，所以個人 repo 裡的 code 和 owner repo 裡的 code 完全沒有相關。

那如何讓它變相關的呢？

這時就是要發出 pull request 給想要讓它有相關的 repo 了。點了pull request 後，會出現左右兩邊的 repo 和 branch。右邊是你的 repo branch，左邊是目標 repo branch。

發出 pull request 的意義就是：

你跟目標 repo 的擁有者說，你有個做好的 branch，想請 owner review，如果 owner 覺得沒問題的話，就可以 merge 到 owner repo branch 了。擁有者收到 pull request 就可以到 tab 的 pull request 去 review，喜歡可以線上直接 merge，覺得有問題就利用 comment 功能來討論。

要注意的是，在 accept 後還是要再重新 fetch。

因為剛剛有提過 clone 是完全不同的 repo 了，而擁有者 accept 只會把它個人的 repo 做 merge，當然還是需要去擁有者那把最新的版本 fetch 下來才能繼續處理下一個 issue。實際的做法，其實只是把擁有者的 remote 加入 local repo 就可以了。

這個方法不但可以解決第一個問題，同時第二個問題也解決了。

另外，fork 還有一個有趣的功能就是：

因為有建立 repo 間的連結，所以在 pull request 時，它可以選擇所有有 fork 過的 user repo。在 user 之間要互相支援時，也能簡單達成。

在 pull request 時別忘了一個重點：在 team work 的時候，commit 是要給整個 team 看的，不是給自己看的。要發 pull request 前，建議還是先用 rebase 整理好。

## Issues Tracker

大部分的專案管理軟體都會有問題追蹤器，可以在專案裡控管 issue 始末和 user 配置。在 GitHub 可以做到如：

* *Create issue*，包括 title 和 description
* *Comment issue*，可以做 discussion
* *Issue's label*，label name 可以自己定義，如：問題、bug、功能等
* *Assign issue*，可以把 issue 指派給特定 user，當然也會通知該 user
* *Milestone*，可以把多個 issue 指定給該 milestone，它也會有進度條的顯示
* *Filter* *Search* *Sort* *Batch process* 等，都是它的基本功能
* [GitHub官網介紹](https://github.com/blog/411-github-issue-tracker)

以上都是專案管理軟體所需要的必備功能，那 GitHub 有比較特別的是：

* 可以上傳附圖 [Issue attachments](https://help.github.com/articles/issue-attachments)
* 在 commit message 裡可以加入特定的關鍵字，在 push 的時候，它就會依照關鍵字的意思去做對應的處理。如 [Closing issues via commit messages](https://help.github.com/articles/closing-issues-via-commit-messages)。

詳細專案管理如何操作就不介紹了，這只是介紹 GitHub 專案管理的功能。

## Gist

有時候寫個程式只是一小片段，並不是完整的一個專案，如排序演算法。這時就可以利用 GitHub 提供的 [Gist](https://gist.github.com/) 服務來做簡單的程式。

Gist 提供的服務：

* Javascript embed
* Source code highlight
* 可包含數個檔案。
* 一個 Gist 就會有一個 repo，也就是可以做 VCS。
* Discussion，也就是留言討論的功能。

那會有什麼好處呢？

在 Facebook 討論程式雖然很方便，但是 Facebook 對於 source code 的版本管理和原始碼 highlight 就不如 Gist 了。那倒不如就是貼個 link，讓其他人可以去 preview 程式碼，而且還能有 VCS 功能。

壞處大概就是：

* 會多一個動作（點 link 的動作）
* 非會員沒有 Discussion 功能

## Topic

* [Multiple Accounts](git/github-multiple-accounts.md)
* [Keep a CHANGELOG](http://keepachangelog.com/zh-TW/0.3.0/)
