# CheatSheet

## Clone

```bash
svn checkout <remote>   # Form remote
```

## Status

```bash
svn status         # working copy 狀態
svn status -u      # 查看 server repo 檔案更新狀態
```

## Add 

```bash
svn add <file>                                              # add to repo
svn status | grep "^\?" | awk '{print $2}' | xargs svn add  # Add all unversioned files
```

## Diff

```bash
svn diff                              # 查看目前目錄與目前版本的差異
svn diff -r <rev>                     # 查看目前目錄與<rev>的差異
svn diff -c <rev>                     # 相當於 git show <commit>
svn diff -r <rev>:<rev> --summarize   # 列出檔案異動清單
```

## Log

```bash
svn log -l 10           # 前 10 筆log
```

## Revert

```bash
svn revert <file>
svn revert -R .                                   # recurse
svn revert --depth infinity <directory name>
```

## Changelist

```bash
svn changelist cl_name <file><file><file>               # 加入
svn changelist cl_name --recursive <folder_name>        # 加入

svn st --changelist cl_name                             # 查詢
svn commit --changelist cl_name -m “xxx”                # commit

svn changelist --remove --recursive --cl cl_name .      # 刪除單一個 changelist
svn changelist --remove --recursive .                   # 刪除所有 changelist      
```

## Conflict

```bash
svn resolve --accept=working <files>
```

## Show ignore

```bash
svn proplist -v
svn propget svn:ignore -R
svn propset svn:ignore "ignoreThis.txt" .   # Apply the svn:ignore property to the current directory.

svn propdel svn:ignore . # For directory 
svn propdel svn:ignore -R # For recursive
```
