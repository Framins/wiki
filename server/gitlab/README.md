# GitLab

[Gitlab](https://www.gitlab.com/) 是一套 open source 的 Git 專案管理系統。其實就很像 [GitHub](https://github.com/) 的 Open Source 版。自己架設起來的話，等於有自己的 Git Server 了。

Gitlab 表面是使用 Rails 做網頁和專案管理，而背後是使用 [grit](https://github.com/mojombo/grit)（一個用 Ruby 寫的 Git 操作 Library） + [Gitlab Shell](https://github.com/gitlabhq/gitlab-shell)（Git Repositories 存取控制系統）來存取檔案層的 Git Repository。

* [Installation](installation.md)

## Compare with Redmine

與 [Redmine](/server/redmine) 的比較

|  GitLab  |  Redmine  |
|  ------  |  -------  |
| 架構較單純，功能陽春，簡單易學 | 架構較複雜，功能完整，複雜難學 |
| 只有單純的 Issue tracker 和 milestone | 專案管理功能超級完整，包括流程定義、時數消耗、版本藍圖等 |
| 內建 git ssh 和 https 功能 | 無內建 git 功能，需用套件另外處理 |
| 因有內建 git，所以原始碼跟 issue tracker 可以直接連結整合 | 同上，雖然它可以直接設定 repo 就能載入 source code，不過會遇上一堆不科學的問題 |
| 可以對 `commit` / `file` / 甚至是某一行 `code` 做 comment | Redmine 好像也可以... 不過上面的問題先解決再說 |
| 內建 repo 權限控管，可參考[這裡](https://gitlab.com/help/permissions/permissions) | 視另外用的整合套件而定 |
| 只有英文介面，除非改 source code | 有中文介面 |
| Project / Issue 無法拆分 | Project / Issue 可拆分 (也就是可以實現子專案 / 子任務) |
