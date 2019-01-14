# Docker Machine

[Docker Machine][] 主要功能是 provision docker engine ，包括 [Swarm](swarm.md) 的應用也可以 provision 。

## Setup

跟 [Compose](compose.md) 一樣，可以直接從 git 上下載可執行檔

    curl -L https://github.com/docker/machine/releases/download/v0.7.0/docker-machine-`uname -s`-`uname -m` > /usr/local/bin/docker-machine
    chmod +x /usr/local/bin/docker-machine

## Quick Start

`create` 指令可以直接 provision 機器， `--driver` 參數為必要，會決定要建機器在哪個地方，以下以 [Google Cloud Platform][] 為例

首先先用 [gcloud](https://cloud.google.com/sdk/) 登入

    gcloud auth login

接著要準備幾個參數，也可以用環境變數，這些參數在 Google 官方網站上建實體的時候都可以參考得到

* **GOOGLE_PROJECT:** 每個 Project 都有唯一的 ID
* **GOOGLE_MACHINE_TYPE:** 建機器的時候，可以設定該機器的等級，這裡用最小的 `f1-micro`
* **GOOGLE_DISK_SIZE:** 磁碟大小，用預設的 `10`
* **GOOGLE_DISK_TYPE:** 磁碟類型，用預設的 `pd-standard`
* **GOOGLE_ZONE:** 要放在 Google 的哪個區，這裡放 `asia-east1-c`

Hint: 其他參數可以直接下 `docker-machine create --driver google` 或是上 [Docker 官網參考](https://docs.docker.com/machine/drivers/gce/)

另外還可以加 [Swarm](swarm.md) 的初始化 `--swarm-master` ，最後則是該實體的名稱

最後指令如下

    docker-machine create --driver google --google-project swarm-test-141105 --google-machine-type f1-micro --google-zone asia-east1-c --swarm-master swarm-master

[Google Cloud Platform]: https://cloud.google.com/
[Docker Machine]: https://docs.docker.com/machine/
