
### Add

https://medium.com/@nareerat.prr/adding-a-new-disk-creating-new-partitions-and-auto-mounting-centos7-c672fa66c50c

```
# fdisk /dev/sda
> n
> p
> 1
> enter
> enter
> w

# pvcreate /dev/sda
# vgcreate datavg /dev/sda
# lvcreate -L 5G -n dataapps dataavg
# mkfs.ext4 /dev/mapper/dataavg-dataapps
```

```
# vi /etc/fstab
/dev/mapper/dataavg-dataapps  /data  ext4  defaults 1 2
```

```
# syncs data to new directory
# rsync -av /state/partition1/apps/* /data/apps/

### Combine
```
# umount /galaxy 
# lvchange -a n /dev/rocks_galaxy/home
# lvremove /dev/rocks_galaxy/home 
# lvextend -l +100%FREE /dev/rocks_galaxy/root
# resize2fs /dev/rocks_galaxy/root
# xfs_growfs /dev/centos/root
```
