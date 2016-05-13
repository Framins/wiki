Rancher
=======

Quick Start
-----------

先用 Docker 安裝 server

```bash
docker run -d --name rancher --restart=always -p 80:8080 rancher/server
docker logs -f rancher-server
```

這樣這台電腦就可以當成是管理端的 server 了，可以用 web 去開，裡面會要求加 host 。加 host 的方式也很簡單，只要上去下一行指令就行了

接著要建立他的代理 server ，執行 docker

```bash
docker run -d --privileged -v /var/run/docker.sock:/var/run/docker.sock rancher/agent:v0.7.10 http://192.168.30.206:8080/v1/scripts/<token>
```

官網也有建議加 IP 參數

```bash
docker run -e CATTLE_AGENT_IP=192.168.1.1 -d --privileged -v /var/run/docker.sock:/var/run/docker.sock rancher/agent:v0.7.10 http://172.17.0.3:8080/v1/scripts/<token>
```
