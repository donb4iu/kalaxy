# CEPH

   
## Setup storage devices   
   
sudo parted -l

**dbuddenbaum@arm64-worker-02:~$**

sudo parted /dev/sda

```
GNU Parted 3.3
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) mklabel gpt
Warning: The existing disk label on /dev/sda will be destroyed and all data on this disk will be lost. Do you want to continue?
Yes/No? yes
(parted) print
Model: APPLE HD D ST1000DM003 (scsi)
Disk /dev/sda: 1000GB
Sector size (logical/physical): 512B/4096B
Partition Table: gpt
Disk Flags:

Number  Start  End  Size  File system  Name  Flags

(parted) mkpart primary ext4 1MB 31.9GB
(parted) print
Model: APPLE HD D ST1000DM003 (scsi)
Disk /dev/sda: 1000GB
Sector size (logical/physical): 512B/4096B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name     Flags
 1      1049kB  31.9GB  31.9GB  ext4         primary

(parted) quit
Information: You may need to update /etc/fstab.
```

**dbuddenbaum@arm64-worker-02:~$**
 
sudo fdisk /dev/sda

```
Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): n
Partition number (2-128, default 2):
First sector (62304256-1953525134, default 62304256):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (62304256-1953525134, default 1953525134):

Created a new partition 2 of type 'Linux filesystem' and of size 901.8 GiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```
