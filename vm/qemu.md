# QEMU

與 VirtualBox 等其他虛擬機不同的是，QEMU 可以模擬 CPU 硬體核心。想當然爾，一定會很慢。

以下筆記是使用 MacOS + QEMU 模擬 Raspberry Pi ARM CPU + raspbian jessie 系統。

首先要先安裝 QEMU

```
brew install qemu
```

再來要來[這裡](https://github.com/dhruvvyas90/qemu-rpi-kernel)下載 Raspberry Pi kernel。這裡的 kernel 必須與下面的作業系統是對應的。（裡面的 README 也有說明）

接著到 [Raspberry Pi 官網](https://downloads.raspberrypi.org/raspbian/images/)下載作業系統映像檔。

> 以下使用 `kernel-qemu-4.4.34-jessie` + `2019-04-08-raspbian-stretch.zip`

下載完後，先解壓縮 zip

```
$ unzip 2019-04-08-raspbian-stretch.zip
Archive:  2019-04-08-raspbian-stretch.zip
  inflating: 2019-04-08-raspbian-stretch.img
```

準備齊全後，就可以啟動 QEMU 了：

```
qemu-system-arm \
  -kernel kernel-qemu-4.4.34-jessie \
  -cpu arm1176 -m 256 \
  -M versatilepb -no-reboot -serial stdio \
  -append "root=/dev/sda2 panic=1 rootfstype=ext4 rw init=/bin/bash" \
  -drive "file=2019-04-08-raspbian-stretch.img,index=0,media=disk,format=raw"
```

啟動後，因預設的設定並不適合 QEMU 執行，所以要進去裡面調整設定：

```
sed -i -e 's/^/#/' /etc/ld.so.preload
sed -i -e 's/^/#/' /etc/ld.so.conf
sed -i -e 's/^/#/' /etc/fstab
```

再次啟動 QEMU：

```
qemu-system-arm
  -kernel kernel-qemu-4.4.34-jessie 
  -cpu arm1176 -m 256 
  -M versatilepb -no-reboot -serial stdio 
  -append "root=/dev/sda2 panic=1 rootfstype=ext4 rw" 
  -drive "file=2017-03-02-raspbian-jessie.img,index=0,media=disk,format=raw" 
  -net user,hostfwd=tcp::5022-:22
```

這裡多加了一個 port forwarding 設定，接著就能使用 ssh 進入機器了：

```
ssh -p 5022 pi@localhost
```

## References

* https://gist.github.com/hfreire/5846b7aa4ac9209699ba
