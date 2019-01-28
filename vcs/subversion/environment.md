# Environment

與 [Git](/vcs/git/README.md) 不一樣的是，Subversion 是屬於中央集權式的控管方法，所以會需要準備一台 server 才能開始 commit，而 client 使用指令去跟 server 互動，所以它跟 [Docker](/docker/README.md) 一樣是標準的 client-server 架構。

## Server

使用 Docker 可以輕鬆建置環境，目前有 [garethflowers/svn-server](https://hub.docker.com/r/garethflowers/svn-server/) 與 [elleflorio/svn-server](https://hub.docker.com/r/elleflorio/svn-server/) 可以用，差別在於前者沒有做 [HTTP Basic authentication][]，後者有。如果想快速開始的話，可以選擇前者。

```
docker run -d --name some-svn -p 3690:3690 garethflowers/svn-server
docker exec -it some-svn sh

# 進入 docker

# 建立新的 repo 名叫 new-repo
svnadmin create new-repo

# 把 anon-access 註解打開，並改成 write，這樣不需要帳密就能 commit 了
vi new-repo/conf/svnserve.conf
```

## Client

Mac 有內建 `svn` 指令，可以直接用。也可以使用 brew 裝 Subversion 的 server，同時裡面會有內建 bash completion ：

```
brew install subversion
```

接著，使用 `svn checkout` 把剛剛 server 所建立的 `new-repo` 拉到本機：

```
svn checkout svn://localhost:3690/new-repo
```

再來就可以再 new-repo 目錄下使用 svn 的功能了。

## References

* [5-使用docker-svn镜像](https://www.jianshu.com/p/0146b5ba69a6)

[HTTP Basic authentication]: https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Authentication
