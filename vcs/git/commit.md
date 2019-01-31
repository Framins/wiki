# Commit

Commit 對 git 而言，就像是 check point 一樣，有了 commit，就可以做以下事情：

* 查詢該 commit 的狀態
* 該 commit 與其他 commit 的差異
* 重置工作目錄到該 commit 的狀態

## Overview

使用 git，當想要 commit 一個版本時，需要做三個步驟：

1. 把檔案加入緩衝區 (staging)
2. 把緩衝區的檔案 commit 到 local repository
3. push commit 到 remote repository
