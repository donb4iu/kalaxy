# Installation Notes

## Raspberry Pi Monitoring

```
sudo apt-get update && sudo apt-get install htop -y
```

## make up
```
xcode-select --install
```

![clusterUp](images/cluster-initial-up.png)

## Flash

```bash
flash \
    --userdata setup/cloud-config.yml \
    ~/Downloads/ubuntu-20.04-preinstalled-server-arm64+raspi.img
    
```

## AMD64

### static ip
sudo vim /etc/netplan/01-netcfg.yaml

```

      network:
        version: 2
        ethernets:
          eth0:
            dhcp4: false
            addresses: [192.168.2.5?/24]
            gateway4: 192.168.2.253
            nameservers:
              addresses: [8.8.8.8, 4.4.4.4]

```
- sudo netplan apply
- ip address

### ssh
- sudo apt install ssh
- sudo systemctl enable --now ssh
- sudo systemctl status ssh

### swapfile

- sudo vim /etc/fstab 
```
#/swapfile

```
- sudo reboot

### update/upgrade

- sudo apt-get update
- sudo apt update
- sudo apt upgrade

### SUDO

sudo visudo

```

dbuddenbaum     ALL=(ALL) NOPASSWD=ALL

```
**dbuddenbaum@amd64-worker-03:~$** sudo vim /etc/sysctl.d/99-kubernetes-cri.conf
```
net.bridge.bridge-nf-call-iptables=1
/usr/sbin/sysctl net.bridge.bridge-nf-call-iptables=1
/usr/sbin/sysctl/net.bridge.bridge-nf-call-iptables=1
net.bridge.bridge-nf-call-ip6tables=1
net.bridge.bridge-nf-call-arptables=1
```
sudo modprobe br_netfilter

**dbuddenbaum@amd64-worker-03:~$** echo "deb http://packages.azlux.fr/debian/ buster main" | sudo tee /etc/apt/sources.list.d/azlux.list
```
deb http://packages.azlux.fr/debian/ buster main

```
**dbuddenbaum@amd64-worker-03:~$** wget -qO  - https://azlux.fr/repo.gpg.key | sudo apt-key add -
```
OK
```
**dbuddenbaum@amd64-worker-03:~$** sudo apt update
```
Hit:1 http://us.archive.ubuntu.com/ubuntu focal InRelease
Building dependency tree
Reading state information... Done
All packages are up to date.
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu focal InRelease' doesn't support architecture 'i386'
```
**dbuddenbaum@amd64-worker-03:~$** sudo apt install log2ram
```
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required:
  conntrack cri-tools ebtables socat
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  log2ram
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 4288 B of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 http://packages.azlux.fr/debian buster/main amd64 log2ram all 1.6.0 [4288 B]
Fetched 4288 B in 1s (7037 B/s)
Selecting previously unselected package log2ram.
(Reading database ... 107469 files and directories currently installed.)
Preparing to unpack .../archives/log2ram_1.6.0_all.deb ...
Unpacking log2ram (1.6.0) ...
Setting up log2ram (1.6.0) ...
Created symlink /etc/systemd/system/sysinit.target.wants/log2ram.service → /etc/systemd/system/log2ram.service.
Created symlink /etc/systemd/system/timers.target.wants/log2ram-daily.timer → /etc/systemd/system/log2ram-daily.timer.
#####         Reboot to activate log2ram         #####
##### edit /etc/log2ram.conf to configure options ####
```


make OPTS=--limit=amd64-worker-xx up