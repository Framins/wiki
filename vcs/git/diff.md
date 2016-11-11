diff
====

git diff 是個功能強大的指令。它可以做到：

* 跟前一個版本的差異
* 兩個版本的差異

比較兩個檔案之間的差異性，通常「兩個檔案的比較」指的是同一個檔案比較不同版本或不同歷史記錄。

* [技巧：Vimdiff 使用](http://www.ibm.com/developerworks/cn/linux/l-vimdiff/)

Other Tools
-----------

[Diffmerge](http://www.sourcegear.com/diffmerge/) ，支援 Windows, Mac, Linux 的視覺 diff 工具。

參考網頁：

* [How to setup Git to use Diffmerge](http://adventuresincoding.com/2010/04/how-to-setup-git-to-use-diffmerge)
* [DiffMerge: 一套不錯的 Diff 軟體, 支援 Windows, Mac, Linux](http://www.haostudio.idv.tw/blog/?p=211)

### Linux

設定參考網頁：[How to setup Git to use Diffmerge](http://adventuresincoding.com/2010/04/how-to-setup-git-to-use-diffmerge)

設定比對的方法：

```bash
git config --global diff.tool diffmerge
git config --global difftool.diffmerge.cmd 'diffmerge "$LOCAL" "$REMOTE"'
git config --global merge.tool diffmerge
git config --global mergetool.diffmerge.cmd "diffmerge --merge --result=\$MERGED \$LOCAL \$BASE \$REMOTE"
git config --global mergetool.diffmerge.trustExitCode true
```

diff 操作：

```bash
# [目前版本] 與 [目前修改] 作比較，沒有差異的話就不會顯示訊息
git difftool <file>

# [該 branch 版本] 與 [目前修改] 作比較
git difftool <branch> <file>

# [branch1 版本] 與 [branch2 版本] 作比較
git difftool <branch1>..<branch2> <file>
```

如果遇到衝突需要解決的時候，下這個指令：

```bash
git mergetool
```

### Mac

設定參考網頁：[Using DiffMerge as your Git visual merge and diff tool](http://twobitlabs.com/2011/08/install-diffmerge-git-mac-os-x/)

設定比對的方法：

```bash
git config --global diff.tool diffmerge
git config --global difftool.diffmerge.cmd 'diffmerge "$LOCAL" "$REMOTE"'
git config --global merge.tool diffmerge
git config --global mergetool.diffmerge.cmd 'diffmerge --merge --result="$MERGED" "$LOCAL" "$(if test -f "$BASE"; then echo "$BASE"; else echo "$LOCAL"; fi)" "$REMOTE"'
git config --global mergetool.diffmerge.trustExitCode true
```

diff 操作：

```bash
# [目前版本] 與 [目前修改] 作比較，沒有差異的話就不會顯示訊息
git difftool <file>

# [該 branch 版本] 與 [目前修改] 作比較
git difftool <branch> <file>

# [branch1 版本] 與 [branch2 版本] 作比較
git difftool <branch1>..<branch2> <file>
```

如果遇到衝突需要解決的時候，下這個指令：

```bash
git mergetool
```

Reference
---------

* [Visual Diff Tools in Linux](http://amjith.blogspot.tw/2007/07/visual-diff-tools-in-linux.html)
* https://blog.longwin.com.tw/2015/01/icdiff-linux-mac-diff-tool-2014/
