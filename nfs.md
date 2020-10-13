# NFS
- [Turn your Raspberry Pi homelab into a network filesystem](https://opensource.com/article/20/5/nfs-raspberry-pi)
- [How To Set Up an NFS Mount on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-20-04)
- [macOS X Mount NFS Share / Set an NFS Client](https://www.cyberciti.biz/faq/apple-mac-osx-nfs-mount-command-tutorial/)
## ubuntu server

- sudo apt update
- sudo apt install nfs-kernel-server
- sudo mkdir /nfs-server/
- sudo chmod -R 777 /nfs-server/

**dbuddenbaum@DONB-ET1831:/media/dbuddenbaum/Sabrent-2tb-nfs$** sudo vi  /etc/exports
```
/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server *(rw,sync,no_subtree_check)

```
-  sudo systemctl restart nfs-server.service

## mac osx client

```
sudo mkdir /private/nfs
sudo mount -t nfs -o resvport,rw DONB-ET1831:/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server /private/nfs

```

**[21:38:24]donbuddenbaum@donbs-iMac:/private/nfs$** showmount -e donb-et1831
```
Exports list on donb-et1831:
/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server *
```


## unbuntu 20.04 client

mkdir -p /mnt/nfs/home
sudo mount -v 192.168.2.112:/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server /mnt/nfs/home -o nfsvers=3