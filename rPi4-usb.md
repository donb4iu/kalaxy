# Move /Var to USB

## remove ceph OSD pods

**#( 05/07/21@ 4:39PM )( dbuddenbaum@dbuddenbaum-mbp ):~**

   kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=0
   ```
deployment.apps/rook-ceph-operator scaled
```
**#( 05/07/21@ 5:00PM )( dbuddenbaum@dbuddenbaum-mbp ):~**

   kubectl -n rook-ceph scale deployment rook-ceph-osd-5 --replicas=0
   ```
deployment.apps/rook-ceph-osd-8 scaled
```
**#( 05/07/21@ 5:02PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**

   kubectl create -f osd-purge.yaml
   ```
Error from server (AlreadyExists): error when creating "osd-purge.yaml": jobs.batch "rook-ceph-purge-osd" already exists
```
**#( 05/07/21@ 5:03PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   
   kubectl -n rook-ceph logs -l app=rook-ceph-purge-osd

## Setup storage devices 

**dbuddenbaum@amd64-03:~$**
 
 sudo umount /mnt/ssd
 
**dbuddenbaum@amd64-03:~$**
 
 sudo mkfs.xfs /dev/sda1 -f
 
    meta-data=/dev/sdb1              isize=512    agcount=4, agsize=1953088 blks
             =                       sectsz=512   attr=2, projid32bit=1
             =                       crc=1        finobt=1, sparse=1, rmapbt=0
             =                       reflink=1
    data     =                       bsize=4096   blocks=7812352, imaxpct=25
             =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
    log      =internal log           bsize=4096   blocks=3814, version=2
             =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0

**dbuddenbaum@amd64-03:~$**
 
 lsblk -f
 
    NAME   FSTYPE         LABEL UUID                                 FSAVAIL FSUSE% MOUNTPOINT
    sda
    ├─sda1 vfat                 6B71-1BD1                               511M     0% /boot/efi
    ├─sda2
    └─sda5 ext4                 36a22861-fc41-44c0-a77f-3f7320e4a78d   89.9G    12% /
    sdb
    ├─sdb1 xfs                  1a0f5b3e-dbfc-4f34-bbf4-7d68798aaf09
    └─sdb2 ceph_bluestore
    sr0
    
**dbuddenbaum@amd64-03:~$**
 
 sudo mount /dev/sda1 /mnt/ssd

**dbuddenbaum@arm64-worker-04:~$** 

sudo fdisk /dev/sda

```
Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): d
Partition number (1,2, default 2):

Partition 2 has been deleted.

Command (m for help): n
Partition number (2-128, default 2):
First sector (67110912-1953525134, default 67110912):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (67110912-1953525134, default 1953525134): +68G

Created a new partition 2 of type 'Linux filesystem' and of size 68 GiB.

Command (m for help): n
Partition number (3-128, default 3):
First sector (209717248-1953525134, default 209717248):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (209717248-1953525134, default 1953525134):

Created a new partition 3 of type 'Linux filesystem' and of size 831.5 GiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

dbuddenbaum@arm64-worker-04:~$ lsblk -f
NAME        FSTYPE   LABEL       UUID                                 FSAVAIL FSUSE% MOUNTPOINT
loop0       squashfs                                                        0   100% /snap/core18/1990
loop1       squashfs                                                        0   100% /snap/core18/2002
loop2       squashfs                                                        0   100% /snap/snapd/11408
loop3       squashfs                                                        0   100% /snap/snapd/11584
loop5       squashfs                                                        0   100% /snap/lxd/19648
loop6       squashfs                                                        0   100% /snap/lxd/20330
sda
├─sda1
├─sda2
└─sda3
mmcblk0
├─mmcblk0p1 vfat     system-boot B726-57E2                             132.8M    47% /boot/firmware
└─mmcblk0p2 ext4     writable    483efb12-d682-4daf-9b34-6e2f774b56f7    6.1G    75% /
```

## Setup for rPi4

**dbuddenbaum@arm64-worker-04:~$**
 
 sudo mkfs.ext4 /dev/sda2
 
``` 
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 17825792 4k blocks and 4456448 inodes
Filesystem UUID: 78ab6377-d48b-4e4e-bd45-765505f600dd
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
	4096000, 7962624, 11239424

Allocating group tables: done
Writing inode tables: done
Creating journal (131072 blocks): done
Writing superblocks and filesystem accounting information: done
```
    
**dbuddenbaum@arm64-worker-04:~$** 

sudo mkdir /mnt/var

**dbuddenbaum@arm64-worker-04:~$** 

sudo mount /dev/sda2 /mnt/var

**dbuddenbaum@arm64-worker-02:~$**

lsblk -f

```
NAME        FSTYPE   LABEL       UUID                                 FSAVAIL FSUSE% MOUNTPOINT
loop0       squashfs                                                        0   100% /snap/core18/
loop1       squashfs                                                        0   100% /snap/core18/
loop2       squashfs                                                        0   100% /snap/lxd/196
loop3       squashfs                                                        0   100% /snap/snapd/1
loop4       squashfs                                                        0   100% /snap/snapd/1
loop5       squashfs                                                        0   100% /snap/lxd/203
sda
├─sda1      xfs                  b0aa3d60-97a6-4b40-8842-8d4bebab4e49   29.6G     1% /mnt/ssd
├─sda2      ext4                 2fc91f9d-4a66-415d-b5df-7b972264fab2     63G     0% /mnt/var
└─sda3
mmcblk0
├─mmcblk0p1 vfat     system-boot B726-57E2                             132.8M    47% /boot/firmwar
└─mmcblk0p2 ext4     writable    483efb12-d682-4daf-9b34-6e2f774b56f7    8.6G    66% /
```
    
**dbuddenbaum@arm64-worker-04:~$**
 
 sudo vi /etc/fstab
 
    UUID=b0aa3d60-97a6-4b40-8842-8d4bebab4e49       /mnt/ssd       xfs     defaults        0       0
    UUID=2fc91f9d-4a66-415d-b5df-7b972264fab2       /var       ext4     defaults        0       2

**dbuddenbaum@arm64-worker-04:~$**
 
 sudo rsync -aqxP /var/* /mnt/var
 
**dbuddenbaum@arm64-worker-04:~$** 

sudo umount /mnt/var
 
sudo shutdown -r 

**#( 05/07/21@ 5:06PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   
   kubectl delete -f osd-purge.yaml
   ```
job.batch "rook-ceph-purge-osd" deleted
```

**#( 05/07/21@ 7:27PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**

   kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=1
```   
deployment.apps/rook-ceph-operator scaled
```