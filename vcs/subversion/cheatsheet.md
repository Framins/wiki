CheatSheet
==========

Clone
------

```bash
svn checkout <remote>   # Form remote
```

Status
------

```bash
svn status         # working copy 狀態
svn status -u      # 查看 server repo 檔案更新狀態
```g

Add 
------

```bash
svn add <file>                                              # add to repo
svn status | grep "^\?" | awk '{print $2}' | xargs svn add  # Add all unversioned files
```

Diff
----

```bash
svn diff                # 查看目前目錄與目前版本的差異
svn diff -r <rev>       # 查看目前目錄與<rev>的差異
```

Log
---

```bash
svn log -l 10           # 前 10 筆log
```

