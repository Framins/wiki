Docker Machine
==============

[Docker Machine][] 主要功能是 provision docker engine ，包括 [Swarm](swarm.md) 的應用也可以 provision 。

Setup
-----

跟 [Compose](compose.md) 一樣，可以直接從 git 上下載可執行檔

    curl -L https://github.com/docker/machine/releases/download/v0.7.0/docker-machine-`uname -s`-`uname -m` > /usr/local/bin/docker-machine
    chmod +x /usr/local/bin/docker-machine

[Docker Machine]: https://docs.docker.com/machine/
