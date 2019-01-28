# Windows solutions

在 Windows 使用 Docker 「可能」會是件困難的事。

這裡記錄了一些已知的解決方法

## Windows 10 with Native Docker

[官方](http://www.docker.com/products/docker#/windows)已推出 Docker for Windows 原生版，可以直接安裝來用

只是有不算小的限制

> Docker: Requires Microsoft Windows 10 Professional or Enterprise 64-bit

如果符合需求的話，直接安裝應該沒什麼太大的問題

## Windows with VM

官方有提供 [Docker Toolbox](https://www.docker.com/products/docker-toolbox)，它裡面有包含了許多套件。其中有一項是 [VirtualBox](https://www.virtualbox.org/)。是的，它是用 Linux 虛擬機 + Docker 來模擬出本機有 Docker 的環境。

大部分的情況下，不會有什麼問題。只有曾聽說過會有 volume 掛載上的問題。

## Windows with Remote Docker Engine

Warning: **這個方法千萬不要用在正式環境上！！**  
Warning: **這個方法千萬不要用在正式環境上！！**  
Warning: **這個方法千萬不要用在正式環境上！！**

這個方法是 Docker Engine 在遠端而不在本機。適用在規定嚴格，要求使用 Windows VM 又不給開 VM 設定的公司裡。

先開一台 Linux 環境裝好 Docker。懶惰一點可以直接 run [Docker in Docker](dind.md)

    docker run -it -d --privileged -p 2375:2375 docker:1.12-dind

`docker-compose.yml` 範例（也可用在 [Rancher](/container/rancher/README.md) 上）

```yaml
dind:
  ports:
    - 2375:2375/tcp
  tty: true
  image: library/docker:1.12-dind
  privileged: true
  stdin_open: true
```

Windows 裝好 Toolbox 後，確認有 docker 指令

    docker help
    
    理論無法用 ps 指令
    docker ps

接著設定環境變數

    export DOCKER_HOST="tcp://<remote_ip>:2375"
    
    # 應該就可以用 ps 指令了
    docker ps

## FAQs

Volume 掛載的問題

* http://unix.stackexchange.com/questions/292999/mounting-a-nfs-directory-into-host-volume-that-is-shared-with-docker

Windows 一些指令列工具

* [PowerShell](https://github.com/PowerShell/PowerShell) Windows 官方出的 shell 不解釋，但只支援 win 8.1 以上
* [Cygwin](https://www.cygwin.com/)
* [Winpty](https://github.com/rprichard/winpty) 如果需要 `exec -it` 的時候，可能需要這個東西
