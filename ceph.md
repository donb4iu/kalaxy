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

If the FSTYPE field is not empty, there is a filesystem on top of the corresponding device. In this case, you can use sda for Ceph partitions.

**dbuddenbaum@arm64-worker-02:/var/lib$**
 
 lsblk -f
 
``` 
NAME        FSTYPE   LABEL       UUID                                 FSAVAIL FSUSE% MOUNTPOINT
loop0       squashfs                                                        0   100% /snap/core18/1990
loop1       squashfs                                                        0   100% /snap/core18/2002
loop2       squashfs                                                        0   100% /snap/lxd/19206
loop3       squashfs                                                        0   100% /snap/lxd/19648
loop4       squashfs                                                        0   100% /snap/snapd/11584
loop5       squashfs                                                        0   100% /snap/snapd/11408
sda
mmcblk0
├─mmcblk0p1 vfat     system-boot B726-57E2                             132.8M    47% /boot/firmware
└─mmcblk0p2 ext4     writable    483efb12-d682-4daf-9b34-6e2f774b56f7     10G    61% /
```

Preparing the external SSD

Attach the SSD drive to the Raspberry Pi with USB

    The SSD will probably show up as '/dev/sda'.
    sudo mkfs.xfs /dev/sdb1 -f ( this will erase all contents of the SSD ).
    sudo mkdir /mnt/ssd
    sudo mount /dev/sdb1 /mnt/ssd


## disk clean up

**dbuddenbaum@arm64-worker-02:~$**
 
 DISK="/dev/sda"
 
**dbuddenbaum@arm64-worker-02:~$**
 
 sudo sgdisk --zap-all $DISK

``` 
GPT data structures destroyed! You may now partition the disk using fdisk or
other utilities.
```

**dbuddenbaum@arm64-worker-02:/var/lib$**
 
 sudo dd if=/dev/zero of="$DISK" bs=1M count=100 oflag=direct,dsync

``` 
100+0 records in
100+0 records out
104857600 bytes (105 MB, 100 MiB) copied, 6.19267 s, 16.9 MB/s
```

dbuddenbaum@arm64-worker-02:/var/lib$ rm -rf /dev/ceph-*
dbuddenbaum@arm64-worker-02:/var/lib$ rm -rf /dev/mapper/ceph--*


## Rook/Ceph

[How to deploy ROOK with CEPH in Kubernetes](https://d-heinrich.medium.com/how-to-deploy-rook-with-ceph-in-kubernetes-baa5a9183830)

[The Ultimate Rook and Ceph Survival Guide](https://cloudopsofficial.medium.com/the-ultimate-rook-and-ceph-survival-guide-eff198a5764a)

[Build Ceph and Kubernetes Based Distributed File Storage System](https://medium.com/swlh/build-ceph-and-kubernetes-based-distributed-file-storage-system-943da3dd0d24)

[Quick Start](https://rook.github.io/docs/rook/master/ceph-quickstart.html)

[Rook Documentation](https://rook.io/docs/rook/v1.6/ceph-object.html)

[cluster.yaml v1.6 Example](https://github.com/rook/rook/tree/release-1.6/cluster/examples/kubernetes/ceph)

[https://github.com/rook/rook/branches](https://github.com/rook/rook/branches)

[https://github.com/rook/rook/tree/release-1.6](https://github.com/rook/rook/tree/release-1.6)

**#( 04/23/21@ 1:28PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl create -f crds.yaml
```
customresourcedefinition.apiextensions.k8s.io/cephblockpools.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephclients.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephclusters.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephfilesystemmirrors.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephfilesystems.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephnfses.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephobjectrealms.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephobjectstores.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephobjectstoreusers.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephobjectzonegroups.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephobjectzones.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/cephrbdmirrors.ceph.rook.io created
customresourcedefinition.apiextensions.k8s.io/objectbucketclaims.objectbucket.io created
customresourcedefinition.apiextensions.k8s.io/objectbuckets.objectbucket.io created
customresourcedefinition.apiextensions.k8s.io/volumereplicationclasses.replication.storage.openshift.io created
customresourcedefinition.apiextensions.k8s.io/volumereplications.replication.storage.openshift.io created
customresourcedefinition.apiextensions.k8s.io/volumes.rook.io created
```

**#( 04/23/21@12:51PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**
   
   kubectl create -f common.yaml
```
namespace/rook-ceph created
clusterrolebinding.rbac.authorization.k8s.io/rook-ceph-object-bucket created
serviceaccount/rook-ceph-admission-controller created
clusterrole.rbac.authorization.k8s.io/rook-ceph-admission-controller-role created
clusterrolebinding.rbac.authorization.k8s.io/rook-ceph-admission-controller-rolebinding created
clusterrole.rbac.authorization.k8s.io/rook-ceph-cluster-mgmt created
role.rbac.authorization.k8s.io/rook-ceph-system created
clusterrole.rbac.authorization.k8s.io/rook-ceph-global created
clusterrole.rbac.authorization.k8s.io/rook-ceph-mgr-cluster created
clusterrole.rbac.authorization.k8s.io/rook-ceph-object-bucket created
serviceaccount/rook-ceph-system created
rolebinding.rbac.authorization.k8s.io/rook-ceph-system created
clusterrolebinding.rbac.authorization.k8s.io/rook-ceph-global created
serviceaccount/rook-ceph-osd created
serviceaccount/rook-ceph-mgr created
serviceaccount/rook-ceph-cmd-reporter created
role.rbac.authorization.k8s.io/rook-ceph-osd created
clusterrole.rbac.authorization.k8s.io/rook-ceph-osd created
clusterrole.rbac.authorization.k8s.io/rook-ceph-mgr-system created
role.rbac.authorization.k8s.io/rook-ceph-mgr created
role.rbac.authorization.k8s.io/rook-ceph-cmd-reporter created
rolebinding.rbac.authorization.k8s.io/rook-ceph-cluster-mgmt created
rolebinding.rbac.authorization.k8s.io/rook-ceph-osd created
rolebinding.rbac.authorization.k8s.io/rook-ceph-mgr created
rolebinding.rbac.authorization.k8s.io/rook-ceph-mgr-system created
clusterrolebinding.rbac.authorization.k8s.io/rook-ceph-mgr-cluster created
clusterrolebinding.rbac.authorization.k8s.io/rook-ceph-osd created
rolebinding.rbac.authorization.k8s.io/rook-ceph-cmd-reporter created
podsecuritypolicy.policy/00-rook-privileged created
clusterrole.rbac.authorization.k8s.io/psp:rook created
clusterrolebinding.rbac.authorization.k8s.io/rook-ceph-system-psp created
rolebinding.rbac.authorization.k8s.io/rook-ceph-default-psp created
rolebinding.rbac.authorization.k8s.io/rook-ceph-osd-psp created
rolebinding.rbac.authorization.k8s.io/rook-ceph-mgr-psp created
rolebinding.rbac.authorization.k8s.io/rook-ceph-cmd-reporter-psp created
serviceaccount/rook-csi-cephfs-plugin-sa created
serviceaccount/rook-csi-cephfs-provisioner-sa created
role.rbac.authorization.k8s.io/cephfs-external-provisioner-cfg created
rolebinding.rbac.authorization.k8s.io/cephfs-csi-provisioner-role-cfg created
clusterrole.rbac.authorization.k8s.io/cephfs-csi-nodeplugin created
clusterrole.rbac.authorization.k8s.io/cephfs-external-provisioner-runner created
clusterrolebinding.rbac.authorization.k8s.io/rook-csi-cephfs-plugin-sa-psp created
clusterrolebinding.rbac.authorization.k8s.io/rook-csi-cephfs-provisioner-sa-psp created
clusterrolebinding.rbac.authorization.k8s.io/cephfs-csi-nodeplugin created
clusterrolebinding.rbac.authorization.k8s.io/cephfs-csi-provisioner-role created
serviceaccount/rook-csi-rbd-plugin-sa created
serviceaccount/rook-csi-rbd-provisioner-sa created
role.rbac.authorization.k8s.io/rbd-external-provisioner-cfg created
rolebinding.rbac.authorization.k8s.io/rbd-csi-provisioner-role-cfg created
clusterrole.rbac.authorization.k8s.io/rbd-csi-nodeplugin created
clusterrole.rbac.authorization.k8s.io/rbd-external-provisioner-runner created
clusterrolebinding.rbac.authorization.k8s.io/rook-csi-rbd-plugin-sa-psp created
clusterrolebinding.rbac.authorization.k8s.io/rook-csi-rbd-provisioner-sa-psp created
clusterrolebinding.rbac.authorization.k8s.io/rbd-csi-nodeplugin created
clusterrolebinding.rbac.authorization.k8s.io/rbd-csi-provisioner-role created
```
**#( 04/23/21@12:52PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**
   
   kubectl create -f operator.yaml
```
configmap/rook-ceph-operator-config created
deployment.apps/rook-ceph-operator created
```

**#( 04/27/21@11:33AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl -n rook-ceph get pod
```   
NAME                                  READY   STATUS    RESTARTS   AGE
rook-ceph-operator-855f844cf4-hdltl   1/1     Running   0          58s
rook-discover-8vq5g                   1/1     Running   0          56s
rook-discover-hlbj2                   1/1     Running   0          56s
rook-discover-ktmgk                   1/1     Running   0          57s
rook-discover-n28xn                   1/1     Running   0          57s
rook-discover-nmtft                   1/1     Running   0          56s
rook-discover-pczgp                   1/1     Running   0          56s
rook-discover-ph5cc                   1/1     Running   0          56s
rook-discover-vlz89                   1/1     Running   0          57s
rook-discover-zdqzd                   1/1     Running   0          56s
```

**#( 04/23/21@ 1:31PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl create -f cluster.yaml
```
cephcluster.ceph.rook.io/rook-ceph created
```

**#( 04/23/21@ 3:33PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl create -f toolbox.yaml
```   
deployment.apps/rook-ceph-tools created
```

## Rook Tools

**[root@rook-ceph-tools-5b4b587f6b-f6kxc /]#**
 
 ceph status
``` 
   cluster:
     id:     4540e5a9-4563-4bc7-95da-1494b6a32132
     health: HEALTH_WARN
             mons are allowing insecure global_id reclaim
  
   services:
     mon: 3 daemons, quorum a,b,c (age 3m)
     mgr: a(active, since 101s)
     osd: 8 osds: 8 up (since 2m), 8 in (since 2m)
  
   data:
     pools:   1 pools, 1 pgs
     objects: 3 objects, 0 B
     usage:   8.0 GiB used, 5.7 TiB / 5.7 TiB avail
     pgs:     1 active+clean
```             
**[root@rook-ceph-tools-5b4b587f6b-f6kxc /]#**
 
 ceph health detail
```
HEALTH_WARN mons are allowing insecure global_id reclaim; Reduced data availability: 1 pg inactive; OSD count 0 < osd_pool_default_size 3
[WRN] AUTH_INSECURE_GLOBAL_ID_RECLAIM_ALLOWED: mons are allowing insecure global_id reclaim
    mon.a has auth_allow_insecure_global_id_reclaim set to true
    mon.b has auth_allow_insecure_global_id_reclaim set to true
    mon.c has auth_allow_insecure_global_id_reclaim set to true
[WRN] PG_AVAILABILITY: Reduced data availability: 1 pg inactive
    pg 1.0 is stuck inactive for 100m, current state unknown, last acting []
[WRN] TOO_FEW_OSDS: OSD count 0 < osd_pool_default_size 3
```
**[root@rook-ceph-tools-5b4b587f6b-f6kxc /]#**
 
 ceph osd status
 
```
ID  HOST              USED  AVAIL  WR OPS  WR DATA  RD OPS  RD DATA  STATE      
 0  arm64-worker-03  1027M   900G      0        0       0        0   exists,up  
 1  amd64-05         1027M   434G      0        0       0        0   exists,up  
 2  amd64-03         1027M   434G      0        0       0        0   exists,up  
 3  amd64-04         1027M   434G      0        0       0        0   exists,up  
 4  amd64-02         1027M   900G      0        0       0        0   exists,up  
 5  arm64-master-01  1027M   900G      0        0       0        0   exists,up  
 6  arm64-worker-02  1027M   900G      0        0       0        0   exists,up  
 7  arm64-worker-04  1027M   900G      0        0       0        0   exists,up 

```
 
**[root@rook-ceph-tools-5b4b587f6b-f6kxc /]#**
 
 ceph osd pool ls detail
```
pool 1 'device_health_metrics' replicated size 3 min_size 2 crush_rule 0 object_hash rjenkins pg_num 1 pgp_num 1 autoscale_mode on last_change 29 flags hashpspool stripe_width 0 pg_num_min 1 application mgr_devicehealth```
```
**[root@rook-ceph-tools-5b4b587f6b-f6kxc /]#**
 
 rados df
``` 
POOL_NAME              USED  OBJECTS  CLONES  COPIES  MISSING_ON_PRIMARY  UNFOUND  DEGRADED  RD_OPS   RD  WR_OPS      WR  USED COMPR  UNDER COMPR
device_health_metrics   0 B        3       0       9                   0        0         0       0  0 B       3  58 KiB         0 B          0 B

total_objects    3
total_used       8.0 GiB
total_avail      5.7 TiB
total_space      5.7 TiB
```

```

ceph status
ceph osd tree
ceph osd status
ceph osd df
ceph osd utilization

```



##Dashboard


**#( 04/23/21@ 4:14PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl create -f dashboard-loadbalancer.yaml
```   
service/rook-ceph-mgr-dashboard-loadbalancer created
```

**#( 04/23/21@ 4:30PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl -n rook-ceph get service
```   
NAME                                   TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)             AGE
csi-cephfsplugin-metrics               ClusterIP      10.100.195.171   <none>         8080/TCP,8081/TCP   170m
csi-rbdplugin-metrics                  ClusterIP      10.108.25.77     <none>         8080/TCP,8081/TCP   170m
rook-ceph-mgr                          ClusterIP      10.108.34.158    <none>         9283/TCP            151m
rook-ceph-mgr-dashboard                ClusterIP      10.96.193.144    <none>         8443/TCP            151m
rook-ceph-mgr-dashboard-loadbalancer   LoadBalancer   10.104.104.117   192.168.2.16   8443:30942/TCP      12m
rook-ceph-mon-a                        ClusterIP      10.96.20.22      <none>         6789/TCP,3300/TCP   153m
rook-ceph-mon-b                        ClusterIP      10.107.3.18      <none>         6789/TCP,3300/TCP   151m
rook-ceph-mon-c                        ClusterIP      10.107.168.135   <none>         6789/TCP,3300/TCP   151m
rook-ceph-rgw-my-store                 ClusterIP      10.98.124.217    <none>         80/TCP              19m
```

Login Credentials

After you connect to the dashboard you will need to login for secure access. Rook creates a default user named **_admin_** and generates a secret called rook-ceph-dashboard-admin-password in the namespace where the Rook Ceph cluster is running. To retrieve the generated password, you can run the following:

**#( 04/23/21@ 4:24PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl -n rook-ceph get secret rook-ceph-dashboard-password -o jsonpath="{['data']['password']}" | base64 --decode && echo
   
```   
y.lkHZmMQbH7'VM->J$_
```



[ceph dashboard](https://192.168.2.16:8443/#/login?returnUrl=%2Fdashboard)


## CRD Deletion gets stuck

**#( 04/24/21@ 6:09PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl patch crd/cephclusters.ceph.rook.io -p '{"metadata":{"finalizers":[]}}' --type=merge
   
```customresourcedefinition.apiextensions.k8s.io/cephclusters.ceph.rook.io patched```

**#( 04/24/21@ 6:15PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl patch crd/cephobjectstores.ceph.rook.io -p '{"metadata":{"finalizers":[]}}' --type=merge

```customresourcedefinition.apiextensions.k8s.io/cephobjectstores.ceph.rook.io patched```

**#( 04/24/21@ 6:16PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl patch crd/cephobjectstoreusers.ceph.rook.io -p '{"metadata":{"finalizers":[]}}' --type=merge

```customresourcedefinition.apiextensions.k8s.io/cephobjectstoreusers.ceph.rook.io patched```


## Remove storage Host-based cluster

[Ceph OSD Management](https://github.com/rook/rook/blob/master/Documentation/ceph-osd-mgmt.md)

Update your CephCluster CR. Depending on your CR settings, you may need to remove the device from the list or update the device filter. If you are using useAllDevices: true, no change to the CR is necessary.

**_IMPORTANT:_** On host-based clusters, you may need to stop the Rook Operator while performing OSD removal steps in order to prevent Rook from detecting the old OSD and trying to re-create it before the disk is wiped or removed.

### To stop the Rook Operator, run 
```
kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=0
```

**_IMPORTANT:_** You must perform steps below to 
 - (1) purge the OSD and either (2.a) delete the underlying data 
 - (2.b)replace the disk before starting the Rook Operator again.

### Start the Rook operator run:

```
 kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=1.
```

### Purge the OSD from the Ceph cluster
    
OSD removal can be automated with the example found in the [rook-ceph-purge-osd job](https://github.com/rook/rook/blob/{{ branchName }}/cluster/examples/kubernetes/ceph/osd-purge.yaml). 

**_IMPORTANT:_** In the osd-purge.yaml, change the **<OSD-IDs>** to the ID(s) of the OSDs you want to remove.
    
- Run the job: kubectl create -f osd-purge.yaml
- When the job is completed, review the logs to ensure success: kubectl -n rook-ceph logs -l app=rook-ceph-purge-osd
- When finished, you can delete the job: kubectl delete -f osd-purge.yaml
    
If you want to remove OSDs by hand, continue with the following sections. However, we recommend you to use the above-mentioned job to avoid operation errors.

### Remove the OSD

- kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=0
- kubectl -n rook-ceph scale deployment rook-ceph-osd-<ID> --replicas=0
- kubectl create -f osd-purge.yaml
- kubectl -n rook-ceph logs -l app=rook-ceph-purge-osd
- kubectl delete -f osd-purge.yaml
- kubectl delete deployment -n rook-ceph rook-ceph-osd-<ID>
- kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=1


### Replace an OSD

To replace a disk that has failed:

- Run the steps in the previous section to Remove an OSD.
- Replace the physical device and verify the new device is attached.
- Check if your cluster CR will find the new device. If you are using useAllDevices: true you can skip this step. If your cluster CR lists individual devices or uses a device filter you may need to update the CR.
- The operator ideally will automatically create the new OSD within a few minutes of adding the new device or updating the CR. If you don't see a new OSD automatically created, restart the operator (by deleting the operator pod) to trigger the OSD creation.
- Verify if the OSD is created on the node by running ceph osd tree from the toolbox.

Note that the OSD might have a different ID than the previous OSD that was replaced.


## Block Storage

[Get block storage from Ceph](https://itnext.io/deploy-a-ceph-cluster-on-kubernetes-with-rook-d75a20c3f5b1)

**#( 05/02/21@ 5:24PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph@master✗✗✗**

   kubectl apply -f ./rbd/storageclass.yaml
   
```
cephblockpool.ceph.rook.io/replicapool created
storageclass.storage.k8s.io/rook-ceph-block created
``` 


**#( 05/02/21@ 5:29PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/rbd@master✗✗✗**
    
    kubectl get pvc,pv
```  
NAME                              STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS      AGE
persistentvolumeclaim/mongo-pvc   Bound    pvc-84409028-a00e-4936-bcf0-63ff36068893   5Gi        RWO            rook-ceph-block   32s

NAME                                                        CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                              STORAGECLASS      REASON   AGE
persistentvolume/pvc-6396501d-8a0b-46aa-a576-a6218908683e   8Gi        RWO            Delete           Bound    monitor/prometheus-server          nfs-ssd1                   131d
persistentvolume/pvc-786f572c-e95c-4556-839a-5081bfe1a0af   2Gi        RWO            Delete           Bound    monitor/prometheus-alertmanager    nfs-ssd1                   131d
persistentvolume/pvc-84409028-a00e-4936-bcf0-63ff36068893   5Gi        RWO            Delete           Bound    amd64default/mongo-pvc             rook-ceph-block            29s
persistentvolume/pvc-f5ddda65-eeef-41c3-b9c4-da2715b5ac33   1Gi        RWO            Delete           Bound    community-grid/rosettaathomedata   nfs-ssd1                   48d
```  
## Deploy MongoDB Community Edition on CEPH block storage

**#( 05/02/21@ 5:54PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/rbd@master✗✗✗**
  
   kubectl apply -f mongo.yaml
``` 
deployment.apps/mongo created
service/mongo created

 ```  
**#( 05/02/21@ 5:54PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/rbd@master✗✗✗**

    kubectl get pods,svc
 ```  
NAME                         READY   STATUS    RESTARTS   AGE
pod/bear-67fd7744bf-f6t9f    1/1     Running   1          4d23h
pod/hare-5446fcff89-jb5zx    1/1     Running   0          4d23h
pod/mongo-5d7ff54f7d-qh67w   1/1     Running   0          32s
pod/moose-57b7db48cb-mx7jc   1/1     Running   1          4d23h

NAME            TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)           AGE
service/bear    ClusterIP   10.105.36.211    <none>        80/TCP            20d
service/hare    ClusterIP   10.101.99.44     <none>        80/TCP            20d
service/mongo   NodePort    10.100.234.50    <none>        27017:31017/TCP   31s
service/moose   ClusterIP   10.108.246.110   <none>        80/TCP            20d
 ```  

**#( 05/02/21@ 5:55PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/rbd@master✗✗✗**

   kubectl get pods  -o wide
``` 
NAME                     READY   STATUS    RESTARTS   AGE     IP              NODE       NOMINATED NODE   READINESS GATES
bear-67fd7744bf-f6t9f    1/1     Running   1          4d23h   10.244.0.104    amd64-02   <none>           <none>
hare-5446fcff89-jb5zx    1/1     Running   0          4d23h   10.244.0.99     amd64-02   <none>           <none>
mongo-5d7ff54f7d-qh67w   1/1     Running   0          9m28s   10.244.12.121   amd64-06   <none>           <none>
moose-57b7db48cb-mx7jc   1/1     Running   1          4d23h   10.244.0.96     amd64-02   <none>           <none>
```

**#( 05/02/21@ 5:54PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/rbd@master✗✗✗**

   kubectl get nodes -o wide

 ```     
NAME              STATUS   ROLES    AGE    VERSION    INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION     CONTAINER-RUNTIME
amd64-02          Ready    master   188d   v1.17.11   192.168.2.56   <none>        Ubuntu 20.04.2 LTS   5.4.0-72-generic   docker://19.3.12
amd64-03          Ready    <none>   188d   v1.17.11   192.168.2.57   <none>        Ubuntu 20.04.2 LTS   5.4.0-72-generic   docker://19.3.12
amd64-04          Ready    <none>   180d   v1.17.11   192.168.2.58   <none>        Ubuntu 20.04.2 LTS   5.4.0-72-generic   docker://19.3.12
amd64-05          Ready    <none>   158d   v1.17.11   192.168.2.59   <none>        Ubuntu 20.04.2 LTS   5.4.0-72-generic   docker://19.3.12
amd64-06          Ready    <none>   50d    v1.17.11   192.168.2.60   <none>        Ubuntu 20.04.2 LTS   5.4.0-72-generic   docker://19.3.12
arm64-master-01   Ready    <none>   69d    v1.17.11   192.168.2.50   <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   docker://19.3.12
arm64-worker-02   Ready    <none>   69d    v1.17.11   192.168.2.52   <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   docker://19.3.12
arm64-worker-03   Ready    <none>   84d    v1.17.11   192.168.2.53   <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   docker://19.3.12
arm64-worker-04   Ready    <none>   69d    v1.17.11   192.168.2.54   <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   docker://19.3.12
 ```   

MongoDB Compass 192.168.2.60:31017