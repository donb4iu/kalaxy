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
## Rook/Ceph

[How to deploy ROOK with CEPH in Kubernetes](https://d-heinrich.medium.com/how-to-deploy-rook-with-ceph-in-kubernetes-baa5a9183830)
[The Ultimate Rook and Ceph Survival Guide](https://cloudopsofficial.medium.com/the-ultimate-rook-and-ceph-survival-guide-eff198a5764a)


[Quick Start](https://rook.github.io/docs/rook/master/ceph-quickstart.html)

[Rook Documentation](https://rook.io/docs/rook/v1.6/ceph-object.html)

[cluster.yaml v1.6 Example](https://github.com/rook/rook/tree/release-1.6/cluster/examples/kubernetes/ceph)

[https://github.com/rook/rook/branches](https://github.com/rook/rook/branches)

[https://github.com/rook/rook/tree/release-1.6](https://github.com/rook/rook/tree/release-1.6)


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
    id:     f75fe9b3-7779-41e6-82c7-7cb52ac8ae31
    health: HEALTH_WARN
            mons are allowing insecure global_id reclaim
            Reduced data availability: 1 pg inactive
            OSD count 0 < osd_pool_default_size 3
 
  services:
    mon: 3 daemons, quorum a,b,c (age 96m)
    mgr: a(active, since 95m)
    osd: 0 osds: 0 up, 0 in
 
  data:
    pools:   1 pools, 1 pgs
    objects: 0 objects, 0 B
    usage:   0 B used, 0 B / 0 B avail
    pgs:     100.000% pgs unknown
             1 unknown
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
 
**[root@rook-ceph-tools-5b4b587f6b-f6kxc /]#**
 
 ceph osd pool ls detail
```
pool 1 'device_health_metrics' replicated size 3 min_size 2 crush_rule 0 object_hash rjenkins pg_num 1 pgp_num 1 autoscale_mode on last_change 11 flags hashpspool,creating stripe_width 0 pg_num_min 1 application mgr_devicehealth
```

**[root@rook-ceph-tools-5b4b587f6b-f6kxc /]#**
 
 rados df
``` 
POOL_NAME              USED  OBJECTS  CLONES  COPIES  MISSING_ON_PRIMARY  UNFOUND  DEGRADED  RD_OPS   RD  WR_OPS   WR  USED COMPR  UNDER COMPR
device_health_metrics   0 B        0       0       0                   0        0         0       0  0 B       0  0 B         0 B          0 B

total_objects    0
total_used       0 B
total_avail      0 B
total_space      0 B
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
dlNt<c,5U!7Ey6q_zo"`
```



[ceph dashboard](https://192.168.2.16:8443/#/login?returnUrl=%2Fdashboard)