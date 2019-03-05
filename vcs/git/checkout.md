# git checkout

如果需要建一個沒有父結點的 branch 可以用這個指令：

    git checkout --orphan <new_branch>

其他常用的指令如下：

```bash
git checkout <branch>                       # 切換到該 branch，如果是本機端無 branch，但遠端有的話會自動建
git checkout -b <branch>                    # 建立並切換到該 branch
git checkout -b <branch> <start-point>      # 建立以 <start-point> 為底的 branch，並切換到該 branch
git checkout --orphan <branch>              # 建立新的 branch 不指向任何 commit，commit 後會成為新的 first commit
git checkout .                              # 還原所有 tracked file
git checkout <file>                         # 還原 <file> 為 HEAD 的狀態
git checkout <tree-ish> [--] <pathspec>     # 把 commit 的檔案 checkout 出來，會無條件覆蓋，所以下這指令前要注意該檔案是否有做過修改
```
