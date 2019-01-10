# Git

[用 Git 寫書的小故事](story.md)

## Roadmap

Git 裡每個東西都是互相有關係，學習上如果能靈活思考，就能更快融入 Git 的世界裡。

以下是參考的 Git 學習路線：

* 基本觀念
  * [VCS 歷史](/vcs/README.md)
  * git graph 理解
  * SHA
  * branch 原理
  * branch to Branch
* 基本指令
  * [Installation](installation.md)
  * [config](config.md)
  * init
  * status
  * add
  * [commit](commit.md)
* 查詢指令
  * status
  * [log](log.md)
  * [reflog](reflog.md)
  * [diff](diff.md)
* 檔案管理
  * add
  * rm (--cache)
  * mv
* 提交管理
  * reset
  * revert
  * cherry-pick
  * rebase
* 分支管理
  * checkout
  * [branch](branch.md)
* 遠端管理
  * remote
  * fetch
  * push
  * pull
  * [clone](clone.md)
* 分支操作
  * merge
  * rebase
* 進階
  * stash
  * submodule
* GitHub/GitLab
  * SSH key
  * create repository
  * push branch
  * remove remote branch
  * pull request
  * [hook](hook.md)

## Git 伺服器選擇

Git 伺服器可以使用公開伺服器，好處是通常會有 Issues Tracker 和 wiki 等模組可以直接使用。壞處是會有限制，解除限制的條件就是要付錢了。

* [GitHub](github.md)
* [BitBucket](bitbucket.md)

如果不想用公開伺服器的話，也可以自行架設伺服器讓團隊的成員來連線使用。通常網路的資料大多都是架設在 Linux 伺服器上的。

* [GitLab](https://about.gitlab.com/)
* [Gogs](https://try.gogs.io/)
* [Gitea](https://gitea.io/)
* [Gitosis](http://git-scm.com/book/en/Git-on-the-Server-Gitosis)
* [Gitolite](http://git-scm.com/book/en/Git-on-the-Server-Gitolite)

或者簡單一點的方法，只要資料夾有共用，其實檔案庫也就等於共用了。

* [Google Drive](https://drive.google.com/)
* [Dropbox](https://www.dropbox.com/)
* [MEGA](https://mega.co.nz/)
* [Box](https://www.box.com/)
* NAS / SMB / FTP / SFTP 等能掛載成連線磁碟機的伺服器。

## Reference

* [ProGit](http://git-scm.com/book) - 官方的學習參考資料
* [GitHub 官方教學](https://try.github.io)
* [30 天精通 Git 版本控管](https://github.com/doggy8088/Learn-Git-in-30-days)
* [Git 版本控制系統](http://ihower.tw/git/) - iHower 大哥寫的 git 教學
* [Git 情境劇](http://blog.gogojimmy.net/2012/02/29/git-scenario/)
* [RabbitVCS](http://rabbitvcs.org/) - Linux 的小烏龜
* [MsysGit](https://gitforwindows.org/) - Git for Windows
* [連猴子都能懂的Git入門指南](http://backlogtool.com/git-guide/tw/)

保留：

* [tree-ish](http://stackoverflow.com/questions/4044368/what-does-tree-ish-mean-in-git)
* [Git caret and tilde](http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde)
