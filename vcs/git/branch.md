branch
======

Branch 的主要指令

|  Usage  |  Description  |
|  -----  |  -----------  |
| `git branch` | 列出目前本機所有的 branch |
| `git branch -r` | 只列出 remote branch |
| `git branch -a` | 列出所有的 branch |
| `git branch -v` | 列出的同時會列出 hash 和 commit message |
| `git branch <branchname>` | 建立以 `<branchname>` 為名的新 branch |
| `git branch <branchname> <start-point>` | 以 `<start-point>` 為基準，建立以 branch name 為名的新 branch，reference 可以是 branch tag commit |
| `git branch -d <branchname>` | 刪除 branch ，如果這 branch 沒被 merge 的話，就不能刪除 |
| `git branch -D <branchname>` | 無條件刪除 branch |

其他跟 branch 相關的指令：

|  Usage  |  Description  |
|  -----  |  -----------  |
| `git push origin :<branchname>` | 刪除遠端分支 |
| `git checkout -b <branchname>` | 建立新的 branch 並切換到該 branch |
