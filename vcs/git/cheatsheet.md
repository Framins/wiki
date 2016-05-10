CheatSheet
==========

Create
------

```bash
git init             # For client
git init --bare      # For server
git clone <remote>   # Form remote
```

Status
------

```bash
git status          # 目前狀態完整版
git status -bs      # 目前狀態簡單版
```

Diff
----

```bash
git diff                # 查看目前目錄與目前版本的差異
git diff --stat         # 簡化成只看檔案行數的增減
git diff <rev>          # 查看目前目錄與<rev>的差異
git diff <rev1> <rev2>  # 查看兩個版本間的差異
```

Log
---

```bash
git log                                       # 顯示目前 branch 直接相關的 log
git log --all                                 # 顯示所有 branch 的 log
git log --graph                               # 節點圖
git log --since="2 weeks ago"                 # 顯示最近2週的log
git log --pretty=short                        # 比預設資訊要再少一點
git log --pretty=oneline                      # 單行簡單顯示，會有 SHA1 和 commit message
git log --pretty=format:"%H %s%n%cn on %ar"   # 自定義顯示
git log -p                                    # 會顯示所有修改過的記錄
git log -p <file>                             # 只限看 <file> 的修改記錄
git log --name-only                           # 顯示 commit 修改過哪些檔案
git blame <file>                              # 顯示該檔案的所有commit記錄
```

<!--

^  git commit  ||
| git add <file> | 新增檔案或修改檔案，都需要用add加入後才會被 commit |
| git rm <file> | 將檔案移除追蹤 |
| git mv <source> <target> | 移動檔案 |
| git commit | |
| git commit -m 'commit message' | |
| git commit -a -m 'commit -message' | 將所有修改過的檔案都 commit |
| git commit -a -v | -v 可以看檔案的詳細改變 |

^  git branch  ||
| git branch | 列出目前本機的 branch |
| git branch -a | 列出所有 branch ，包括 remote |
| git branch <Branch> | 建立新的 branch |
| git branch <Branch> <Base> | 以 <Base> 為底，建立新的 branch |
| git branch -d <Branch> | 刪除 branch |
| git branch -D <Branch> | 強制刪除 branch |
| git branch -f <Branch> <Position> | 強制移動 branch 到指定 commit |
^  git checkout  ||
| git checkout <Branch> | 切換到該branch，如果是本機端無branch，但遠端有的話會自動建 |
| git checkout <SHA/branch/tag> <filename> | 把commit的檔案checkout出來，會無條件覆蓋，所以下這指令前要注意該檔案是否有做過修改 |
| git checkout -b <Branch> | 建立並切換到該branch |
| git checkout -b <Branch> <Base> | 建立以<Base>為底的branch，並切換到該branch |
| git checkout <file> | 還原<file>為目前repository的狀態 |
| git checkout . | 還原所有tracked file |
^  git merge  ||
| %%git merge --abort%% | 取消merge |
^  git rebase  ||
| %%git rebase --abort%% | 取消rebase |
^  git stash  ||
| git stash | 把目前的修改丟進暫存區 | 
| %%git stash save [-u|--include-untracked]%% | 把所有檔案，包括未追蹤的檔案加入暫存區 |
| git stash list | 列出所有暫存區的資料 |
| git stash pop | 取出最後一筆並移除 |
| git stash apply | 取出最後一筆但不移除 |
| git stash clear | 清除stash |
^  git reset  ||
| git reset <​target>​ | 將目前的 commit 還原，使目錄內檔案回到 <​target>​ 狀態，此變動只影響本機 |
^  git revert  ||
| git revert <​target>​ | reset + commit，所生成的新提交將使其它協作者可見這項變動 |
^  git cherry-pick  ||
| git cherry-pick <​commit1>​ <​commit2>​ <...> | 複製指定 commit，做為目前 commit 下的子提交 |
| git cherry-pick <​branchold>​..<branchnew> | 複製一區段範圍的 commit |

^  git push  ||
| git push | 把本機最新的 commit 同步至遠端 |
| git push origin <target> | 將 <target> 並同步至遠端的 <target>，若遠端沒有的話會自動建 |
| git push origin :<target> | 傳送一個空值，刪除遠端的 <target> |
| git push origin <source>:<target> | 在本地創建一個分支 <target>，使之與遠端的 <source> 連接 |
^  git pull  ||
| git pull | 把遠端最新的 commit Fetch & Merge 回本機 |
| %%git pull --rebase%% | 把遠端最新的 commit Fetch & Rebase 回本機 |
| git pull origin <target> | 只指定 pull <target> 的所有更動 |
| git pull origin :<target> | 傳送一個空值，刪除本機的 <target> |
| git pull origin <source>:<target> | 在遠端創建一個分支 <target>，使之與本機的 <source> 連接 |
^  git fetch  ||
| git fetch | 將遠端所有更新下載回本機 |
| git fetch -p | 將本地端無用的遠端 branch 刪除 |
| git fetch origin <target> | 只指定 fetch <target> 的所有更動 |
| git fetch origin :<target> | 傳送一個空值，在本機增加一個 <target>  |


-->
