# LVM

LVM 是 Linux 系統中內定的磁碟管理方式，只要在安裝系統時沒有特別設定，系統自動會使用 LVM 將磁碟切割為兩部份，一部份開機磁區約100MB，剩下部分為全權交由 LVM 管理

## Extend

用 VMware 發現某虛擬機空間爆了，首先先加磁碟給它，假設是 `/dev/sdb`。新磁碟就是要 `fdisk` 它，不然要幹嘛

```
# fdisk -l /dev/sdb
Disk /dev/sdb: 34.4 GB, 34359738368 bytes
255 heads, 63 sectors/track, 4177 cylinders, total 67108864 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00000000

Disk /dev/sdb doesn't contain a valid partition table

# fdisk /dev/sdb
略，重點是最後的 ID 要是 8e Linux LVM

# fdisk -l /dev/sdb
Disk /dev/sdb: 34.4 GB, 34359738368 bytes
86 heads, 4 sectors/track, 195083 cylinders, total 67108864 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x015f6f08

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048    67108863    33553408   8e  Linux LVM
```

新增 PV

```
# pvs
  PV         VG        Fmt  Attr PSize  PFree 
  /dev/sda5  ubuntu-vg lvm2 a--  15.76g 24.00m

# pvcreate /dev/sdb1
  Physical volume "/dev/sdb1" successfully created

# pvs
  PV         VG        Fmt  Attr PSize  PFree 
  /dev/sda5  ubuntu-vg lvm2 a--  15.76g 24.00m
  /dev/sdb1            lvm2 a--  32.00g 32.00g
```

加入 VG

```
# vgs
  VG        #PV #LV #SN Attr   VSize  VFree 
  ubuntu-vg   1   2   0 wz--n- 15.76g 24.00m

# vgextend ubuntu-vg /dev/sdb1
  Volume group "ubuntu-vg" successfully extended

# vgs
  VG        #PV #LV #SN Attr   VSize  VFree 
  ubuntu-vg   2   2   0 wz--n- 47.75g 32.02g
```

擴大 LV 空間

```
# lvs
  LV     VG        Attr      LSize    Pool Origin Data%  Move Log Copy%  Convert
  root   ubuntu-vg -wi-ao---   14.74g
  swap_1 ubuntu-vg -wi-ao--- 1020.00m

# lvextend /dev/mapper/ubuntu--vg-root /dev/sdb1 
  Extending logical volume root to 46.73 GiB
  Logical volume root successfully resized

# lvs
  LV     VG        Attr      LSize    Pool Origin Data%  Move Log Copy%  Convert
  root   ubuntu-vg -wi-ao---   46.73g
  swap_1 ubuntu-vg -wi-ao--- 1020.00m
```

最後使用 `resize2fs`，將 LV 的實際空間擴大到最大值

```
# resize2fs /dev/mapper/ubuntu--vg-root 
resize2fs 1.42.9 (4-Feb-2014)
Filesystem at /dev/mapper/ubuntu--vg-root is mounted on /; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 3
The filesystem on /dev/mapper/ubuntu--vg-root is now 12251136 blocks long.

# df -h
Filesystem                   Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-root   46G  8.7G   36G  20% /
略...
```

## References

什麼是 PV, VG, LV ? 可以參考鳥哥的文章

http://linux.vbird.org/linux_basic/0420quota.php#lvm_whatis
