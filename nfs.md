# NFS
- [Turn your Raspberry Pi homelab into a network filesystem](https://opensource.com/article/20/5/nfs-raspberry-pi)
- [How To Set Up an NFS Mount on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-20-04)
- [macOS X Mount NFS Share / Set an NFS Client](https://www.cyberciti.biz/faq/apple-mac-osx-nfs-mount-command-tutorial/)
- [Dynamic NFS Provisioning in Kubernetes](https://blog.exxactcorp.com/deploying-dynamic-nfs-provisioning-in-kubernetes/)
## ubuntu server

- sudo apt update
- sudo apt install nfs-kernel-server
- sudo mkdir /nfs-server/
- sudo chmod -R 777 /nfs-server/

**dbuddenbaum@DONB-ET1831:/media/dbuddenbaum/Sabrent-2tb-nfs$** sudo vi  /etc/exports
```
/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server *(rw,sync,no_subtree_check,no_root_squash,no_all_squash,insecure,anonuid=1000,anongid=1000)

```
-  sudo systemctl restart nfs-server.service

## mac osx client

**#( 11/16/20@ 1:53AM )( dbuddenbaum@dbuddenbaum-mbp ):~**
mkdir ~/nfs-dir

**#( 11/16/20@ 1:53AM )( dbuddenbaum@dbuddenbaum-mbp ):~**
mount -t nfs 192.168.2.112:/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server ~/nfs-dir

**#( 11/16/20@ 1:53AM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   ls nfs-dir
```
lost+found nfs-server

```

**[21:38:24]donbuddenbaum@donbs-iMac:/private/nfs$** showmount -e donb-et1831
```
Exports list on donb-et1831:
/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server *
```


## unbuntu 20.04 client

sudo apt update
sudo apt install nfs-common


sudo mkdir -p /mnt/nfs/home
sudo mount -v 192.168.2.112:/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server /mnt/nfs/home -o nfsvers=3



## persistent volume

**#( 10/26/20@ 6:32PM )( donbuddenbaum@donbs-iMac ): ~/Documents/rPi4/kalaxy/yaml@master✗✗✗** kubectl create -f nfs-pv.yaml
```
persistentvolume/nfs-pv created
```

## persistent volume 

**#( 10/26/20@ 6:32PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗** kubectl get pv
```
NAME     CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
nfs-pv   10Gi       RWX            Recycle          Available           nfs                     3m30s
```


## persistent volume claim

** #( 10/26/20@ 6:36PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗ ** kubectl create -f nfs-pvc.yaml
```
persistentvolumeclaim/nfs-pvc created
```

**#( 10/26/20@ 6:38PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗** kubectl get pvc nfs-pvc
```
NAME      STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
nfs-pvc   Bound    nfs-pv   10Gi       RWX            nfs            2m6s
```
**#( 10/26/20@ 6:39PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗** kubectl get pv nfs-pv
```
NAME     CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM             STORAGECLASS   REASON   AGE
nfs-pv   10Gi       RWX            Recycle          Bound    default/nfs-pvc   nfs                     7m33s
```

## mount commands

**#( 11/16/20@12:43AM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   showmount -e 192.168.2.112
```
Exports list on 192.168.2.112:
/media/dbuddenbaum/Sabrent-2tb-nfs/nfs-server *
```

## storage logs 

**#( 11/23/20@12:49AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**
  
   kubectl logs -f nfs-client-provisioner-8cbd9d67c-svl2d -n nfs-storage
   
```
I1116 17:21:41.038864       1 leaderelection.go:185] attempting to acquire leader lease  nfs-storage/nfs-provisioner-nfs-ssd1...
I1116 17:21:41.050908       1 leaderelection.go:194] successfully acquired lease nfs-storage/nfs-provisioner-nfs-ssd1
I1116 17:21:41.051718       1 controller.go:631] Starting provisioner controller nfs-provisioner/nfs-ssd1_nfs-client-provisioner-8cbd9d67c-svl2d_30fd60f6-2830-11eb-8250-9af622c5b843!
I1116 17:21:41.051778       1 event.go:221] Event(v1.ObjectReference{Kind:"Endpoints", Namespace:"nfs-storage", Name:"nfs-provisioner-nfs-ssd1", UID:"a7601751-1136-4424-bd05-c263d481da65", APIVersion:"v1", ResourceVersion:"5569734", FieldPath:""}): type: 'Normal' reason: 'LeaderElection' nfs-client-provisioner-8cbd9d67c-svl2d_30fd60f6-2830-11eb-8250-9af622c5b843 became leader
I1116 17:21:41.151948       1 controller.go:680] Started provisioner controller nfs-provisioner/nfs-ssd1_nfs-client-provisioner-8cbd9d67c-svl2d_30fd60f6-2830-11eb-8250-9af622c5b843!
```

## Service accounts and cluster roles

**#( 11/23/20@ 1:36AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**

   kubectl describe sa -n nfs-storage

```
Name:                default
Namespace:           nfs-storage
Labels:              <none>
Annotations:         <none>
Image pull secrets:  <none>
Mountable secrets:   default-token-nwz62
Tokens:              default-token-nwz62
Events:              <none>


Name:                nfs-client-provisioner
Namespace:           nfs-storage
Labels:              <none>
Annotations:         kubectl.kubernetes.io/last-applied-configuration:
                       {"apiVersion":"v1","kind":"ServiceAccount","metadata":{"annotations":{},"name":"nfs-client-provisioner","namespace":"nfs-storage"}}
Image pull secrets:  <none>
Mountable secrets:   nfs-client-provisioner-token-8cjn8
Tokens:              nfs-client-provisioner-token-8cjn8
Events:              <none>
```

**#( 11/23/20@ 1:39AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**
    kubectl describe clusterrole nfs-client-provisioner
    
```
Name:         nfs-client-provisioner-runner
Labels:       <none>
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"rbac.authorization.k8s.io/v1","kind":"ClusterRole","metadata":{"annotations":{},"name":"nfs-client-provisioner-runner"},"ru...
PolicyRule:
  Resources                      Non-Resource URLs  Resource Names  Verbs
  ---------                      -----------------  --------------  -----
  events                         []                 []              [create update patch]
  persistentvolumes              []                 []              [get list watch create delete]
  persistentvolumeclaims         []                 []              [get list watch update]
  storageclasses.storage.k8s.io  []                 []              [get list watch]
```