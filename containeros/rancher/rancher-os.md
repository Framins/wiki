Rancher OS
==========

安裝方法有兩種

## Vagrant

最簡單的方法，就是用 *Vagrant* ，下載官方的 [GitHub repo](https://github.com/rancher/os-vagrant) 後直接下 `vagrant up` 指令，即可安裝 RancherOS 虛擬機

## From ISO

另一種是 iso 檔安裝，這是相對比較麻煩的方法。不過也可藉此了解一點 RancherOS 的內容和設定方法

1. 首先到官方 [GitHub Release](https://github.com/rancher/os/releases) 頁，下載 ISO
2. 使用此 ISO 開機。開好機後，使用 `rancher/rancher` 登入，預設它的設定和 image 都是存在 memory 的，重開機都會消失，因此要把它裝到磁碟裡
3. 因為測試時環境並沒有 DHCP ，網路連線需要手動調整後才能正常連結，一般只要 IP 和 gateway 調好應該就能連線了

```bash
sudo ifconfig eth0 192.168.1.10
sudo route add default gw 192.168.1.254
```

- 準備一個設定檔 `cloud-config.yml` 。測試時，是把這個 yml 檔放在網路上的空間，之後用 wget 下載來用。這個設定檔有幾個重要的東西要調整：一個是 SSH public key ，另一個是網路設定。因為一開始安裝好後，只能靠 SSH 的方式進去操作系統。沒網路，沒 public key 等同無法操作...以下是一個比較完整的設定範例

```
hostname: rancher-01
ssh_authorized_keys:
  - ssh-rsa ...
rancher:
  network:
    interfaces:
      eth0:
        address: 192.168.1.10/24
        gateway: 192.168.1.254
        dhcp: false
    dns:
      nameservers:
        - 8.8.8.8
```

- 再來就可以安裝了

```bash
sudo rancheros-install -c cloud-config.yml -d /dev/sda
```
- 安裝好後，重開機，就不能再用原本的 `rancher/rancher` 登入了，只能換用 ssh 登入

```bash
ssh rancher@192.168.1.10
```

安裝好後，在裡面操作 Docker 跟平常沒什麼不一樣了。只是會是在 User Docker 裡操作，在裡面看不到 System Docker

使用上，只要專注在操作 Docker 上就好了，不用擔心把系統搞壞。
