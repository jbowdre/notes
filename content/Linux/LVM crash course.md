---
tags:
  - linux
  - disk
  - shell
  - lvm
---
## New partition
1. Use `lsblk` to ID the disk.
2. Create LVM physical disk
  ```shell
  sudo pvcreate /dev/$device     
  ```
3. Create LVM volume group
   ```shell
   sudo vgcreate $vg_name /dev/$device
   ```
4. Create LVM logical volume
  ```shell
  sudo lvcreate -l 100%FREE -n $lv_name $vg_name
  ```
5. Format volume
   ```shell
   sudo mkfs.ext4 /dev/$vg_name/$lv_name
   ```
5. Create mountpoint
   ```shell
   sudo mkdir /$mountpoint
   ```
6. Use `lsblk -f /dev/$device` to find partition UUID
7. Insert UUID into fstab
  ```shell
   sudo vi /etc/fstab
  ```

  ```
  [...]
  UUID=$UUID /$mountpoint ext4 defaults 0 2
  ```
8. Mount all disks
  ```shell
  sudo mount -a
  ```

## Extend partition
1. Scan for new disk devices
```shell
ls /sys/class/scsi_host/ | while read host; do echo "- - -" > /sys/class/scsi_host/$host/scan; done
```
or 
Scan for resized disk (at `/dev/sdb`)
```shell
echo 1 > /sys/block/sdb/device/rescan
```
2. Use `fdisk`/`cfdisk`/`parted` to create new partition
3. Refresh partition table (if `fdisk -l`)
```shell
partx -v -a /dev/sdb
```
4. Resize LVM stuff
```shell
vgextend $vg_name /dev/sdbX
lvextend -l +100%FREE -r /dev/$vg_name/$lv_name
```
The `-r` flag will automatically resize the file system too.

---
See also:
- [[Extend Partition (Windows)]]