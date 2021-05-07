# Upgrading Kubernettes

[Upgrading Kubernettes](https://v1-18.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

## Master 

**dbuddenbaum@amd64-02:~$**
 
 sudo dpkg -l | grep kube
 
``` 
hi  kubeadm                              1.17.11-00                        amd64        Kubernetes Cluster Bootstrapping Tool
hi  kubectl                              1.17.11-00                        amd64        Kubernetes Command Line Tool
hi  kubelet                              1.17.11-00                        amd64        Kubernetes Node Agent
hi  kubernetes-cni                       0.8.6-00                          amd64        Kubernetes CNI
```

**dbuddenbaum@amd64-02:~$**
 
 sudo apt update
 
```
Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Hit:2 http://us.archive.ubuntu.com/ubuntu focal InRelease
Hit:3 https://download.newrelic.com/infrastructure_agent/linux/apt focal InRelease
Get:5 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Hit:6 https://download.docker.com/linux/ubuntu focal InRelease
Get:7 http://packages.cloud.google.com/apt kubernetes-xenial InRelease [9383 B]
Get:8 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]
Hit:9 http://packages.azlux.fr/debian buster InRelease
Get:4 https://packages.cloud.google.com/apt kubernetes-xenial InRelease [9383 B]
Err:7 http://packages.cloud.google.com/apt kubernetes-xenial InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
Get:10 http://us.archive.ubuntu.com/ubuntu focal-updates/main i386 Packages [466 kB]
Get:11 http://us.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [955 kB]
Get:12 http://us.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [768 kB]
Err:4 https://packages.cloud.google.com/apt kubernetes-xenial InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
Get:13 http://us.archive.ubuntu.com/ubuntu focal-updates/universe i386 Packages [567 kB]
Fetched 3098 kB in 4s (782 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
24 packages can be upgraded. Run 'apt list --upgradable' to see them.
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu focal InRelease' doesn't support architecture 'i386'
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://packages.cloud.google.com/apt kubernetes-xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://packages.cloud.google.com/apt kubernetes-xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Failed to fetch http://apt.kubernetes.io/dists/kubernetes-xenial/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Failed to fetch http://packages.cloud.google.com/apt/dists/kubernetes-xenial/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Some index files failed to download. They have been ignored, or old ones used instead.
```

**dbuddenbaum@amd64-02:~$**
 
 sudo apt-cache madison kubeadm
 
 ```
   kubeadm |  1.20.5-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.5-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.4-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.4-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.2-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.2-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.1-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.1-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.0-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.20.0-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.9-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.9-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.8-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.8-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.7-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.7-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.6-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.6-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.5-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.5-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.4-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.4-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.3-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.3-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.2-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.2-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.1-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.1-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.0-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.19.0-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.17-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.17-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.16-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.16-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.15-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.15-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.14-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.14-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.13-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.13-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.12-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.12-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.10-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.18.10-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.9-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.9-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.8-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.8-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.6-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.6-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.5-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.5-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.4-01 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.4-01 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.4-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.4-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.3-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.3-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.2-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.2-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.1-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.1-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.0-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.18.0-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.17-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.17-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.16-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.16-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.15-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.15-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.14-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.14-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.13-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.13-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.12-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.12-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.11-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm | 1.17.11-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.9-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.9-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.8-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.8-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.7-01 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.7-01 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.7-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.7-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.6-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.6-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.5-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.5-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.4-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.4-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.3-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.3-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.2-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.2-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.1-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.1-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.0-00 | http://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
   kubeadm |  1.17.0-00 | http://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages
```

**#( 05/07/21@ 2:05PM )( dbuddenbaum@dbuddenbaum-mbp ):~**

   kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=0
   
```   
deployment.apps/rook-ceph-operator scaled
```

    kubectl create -f osd-purge.yaml


**#( 05/07/21@ 1:49PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/wffh/healthcare-framework@draft✗✗✗**

   kubectl drain amd64-02

```   
node/amd64-02 cordoned
evicting pod "ingestion-fhir-6f94b96865-7c6pc"
evicting pod "coredns-6955765f44-r9gth"
evicting pod "boinc-workers-4hfxp"
evicting pod "bear-67fd7744bf-f6t9f"
evicting pod "coredns-6955765f44-9mn6b"
evicting pod "prometheus-kube-state-metrics-9d68b9bf4-v9r97"
evicting pod "rook-ceph-crashcollector-amd64-02-745f7c9d54-p44kt"
evicting pod "boinc-workers-h7p5r"
evicting pod "rook-ceph-osd-10-59c7487749-h6jqd"
evicting pod "kube-ops-view-6b485f7cc-fwqhc"
evicting pod "moose-57b7db48cb-mx7jc"
evicting pod "rook-ceph-osd-4-6477fcc44-pjpp7"
pod/moose-57b7db48cb-mx7jc evicted
pod/coredns-6955765f44-r9gth evicted
pod/coredns-6955765f44-9mn6b evicted
pod/ingestion-fhir-6f94b96865-7c6pc evicted
pod/rook-ceph-osd-10-59c7487749-h6jqd evicted
pod/rook-ceph-crashcollector-amd64-02-745f7c9d54-p44kt evicted
pod/bear-67fd7744bf-f6t9f evicted
pod/boinc-workers-4hfxp evicted
pod/prometheus-kube-state-metrics-9d68b9bf4-v9r97 evicted
pod/boinc-workers-h7p5r evicted
pod/kube-ops-view-6b485f7cc-fwqhc evicted
```

## 1.17.11 -> 1.18.17

**dbuddenbaum@amd64-02:~$**
 
 sudo apt-get update

``` 
Hit:1 https://download.newrelic.com/infrastructure_agent/linux/apt focal InRelease
Hit:2 https://download.docker.com/linux/ubuntu focal InRelease
Get:3 http://packages.cloud.google.com/apt kubernetes-xenial InRelease [9383 B]
Hit:4 http://packages.azlux.fr/debian buster InRelease
Err:3 http://packages.cloud.google.com/apt kubernetes-xenial InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
Hit:5 http://us.archive.ubuntu.com/ubuntu focal InRelease
Get:7 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:8 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]
Get:6 https://packages.cloud.google.com/apt kubernetes-xenial InRelease [9383 B]
Err:6 https://packages.cloud.google.com/apt kubernetes-xenial InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
Get:9 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Fetched 342 kB in 16s (22.1 kB/s)
Reading package lists... Done
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu focal InRelease' doesn't support architecture 'i386'
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://packages.cloud.google.com/apt kubernetes-xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://packages.cloud.google.com/apt kubernetes-xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Failed to fetch http://apt.kubernetes.io/dists/kubernetes-xenial/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Failed to fetch http://packages.cloud.google.com/apt/dists/kubernetes-xenial/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Some index files failed to download. They have been ignored, or old ones used instead.
```

**dbuddenbaum@amd64-02:~$**
 
 sudo apt-get install -y --allow-change-held-packages kubernetes-cni=0.8.7-00
 
``` 
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following held packages will be changed:
  kubernetes-cni
The following packages will be upgraded:
  kubernetes-cni
1 upgraded, 0 newly installed, 0 to remove and 23 not upgraded.
Need to get 25.0 MB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubernetes-cni amd64 0.8.7-00 [25.0 MB]
Fetched 25.0 MB in 12s (2083 kB/s)
(Reading database ... 144373 files and directories currently installed.)
Preparing to unpack .../kubernetes-cni_0.8.7-00_amd64.deb ...
Unpacking kubernetes-cni (0.8.7-00) over (0.8.6-00) ...
Setting up kubernetes-cni (0.8.7-00) ...
dbuddenbaum@amd64-02:~$ apt-get install -y --allow-change-held-packages kubeadm=1.18.17-00
E: Could not open lock file /var/lib/dpkg/lock-frontend - open (13: Permission denied)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root?
dbuddenbaum@amd64-02:~$ sudo apt-get install -y --allow-change-held-packages kubeadm=1.18.17-00
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following held packages will be changed:
  kubeadm
The following packages will be upgraded:
  kubeadm
1 upgraded, 0 newly installed, 0 to remove and 22 not upgraded.
Need to get 8168 kB of archives.
After this operation, 418 kB of additional disk space will be used.
Get:1 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubeadm amd64 1.18.17-00 [8168 kB]
Fetched 8168 kB in 4s (1875 kB/s)
(Reading database ... 144373 files and directories currently installed.)
Preparing to unpack .../kubeadm_1.18.17-00_amd64.deb ...
Unpacking kubeadm (1.18.17-00) over (1.17.11-00) ...
Setting up kubeadm (1.18.17-00) ...
```

**dbuddenbaum@amd64-02:~$**
 
 kubeadm version
``` 
kubeadm version: &version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.17", GitCommit:"68b4e26caf6ede7af577db4af62fb405b4dd47e6", GitTreeState:"clean", BuildDate:"2021-03-18T01:00:09Z", GoVersion:"go1.13.15", Compiler:"gc", Platform:"linux/amd64"}
```

**dbuddenbaum@amd64-02:~$**  

sudo kubeadm upgrade plan

```
[upgrade/config] Making sure the configuration is correct:
[upgrade/config] Reading configuration from the cluster...
[upgrade/config] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[preflight] Running pre-flight checks.
[upgrade] Running cluster health checks
[upgrade] Fetching available versions to upgrade to
[upgrade/versions] Cluster version: v1.17.13
[upgrade/versions] kubeadm version: v1.18.17
I0507 20:00:42.711803   33477 version.go:255] remote version is much newer: v1.21.0; falling back to: stable-1.18
[upgrade/versions] Latest stable version: v1.18.18
[upgrade/versions] Latest stable version: v1.18.18
[upgrade/versions] Latest version in the v1.17 series: v1.17.17
[upgrade/versions] Latest version in the v1.17 series: v1.17.17

Components that must be upgraded manually after you have upgraded the control plane with 'kubeadm upgrade apply':
COMPONENT   CURRENT        AVAILABLE
Kubelet     9 x v1.17.11   v1.17.17

Upgrade to the latest version in the v1.17 series:

COMPONENT            CURRENT    AVAILABLE
API Server           v1.17.13   v1.17.17
Controller Manager   v1.17.13   v1.17.17
Scheduler            v1.17.13   v1.17.17
Kube Proxy           v1.17.13   v1.17.17
CoreDNS              1.6.5      1.6.7
Etcd                 3.4.3      3.4.3-0

You can now apply the upgrade by executing the following command:

	kubeadm upgrade apply v1.17.17

_____________________________________________________________________

Components that must be upgraded manually after you have upgraded the control plane with 'kubeadm upgrade apply':
COMPONENT   CURRENT        AVAILABLE
Kubelet     9 x v1.17.11   v1.18.18

Upgrade to the latest stable version:

COMPONENT            CURRENT    AVAILABLE
API Server           v1.17.13   v1.18.18
Controller Manager   v1.17.13   v1.18.18
Scheduler            v1.17.13   v1.18.18
Kube Proxy           v1.17.13   v1.18.18
CoreDNS              1.6.5      1.6.7
Etcd                 3.4.3      3.4.3-0

You can now apply the upgrade by executing the following command:

	kubeadm upgrade apply v1.18.18

Note: Before you can perform this upgrade, you have to update kubeadm to v1.18.18.
```

**dbuddenbaum@amd64-02:~$**
 
 sudo kubeadm upgrade apply v1.18.17
 
``` 
[upgrade/config] Making sure the configuration is correct:
[upgrade/config] Reading configuration from the cluster...
[upgrade/config] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[preflight] Running pre-flight checks.
[upgrade] Running cluster health checks
[upgrade/version] You have chosen to change the cluster version to "v1.18.17"
[upgrade/versions] Cluster version: v1.17.13
[upgrade/versions] kubeadm version: v1.18.17
[upgrade/confirm] Are you sure you want to proceed with the upgrade? [y/N]: y
[upgrade/prepull] Will prepull images for components [kube-apiserver kube-controller-manager kube-scheduler etcd]
[upgrade/prepull] Prepulling image for component etcd.
[upgrade/prepull] Prepulling image for component kube-apiserver.
[upgrade/prepull] Prepulling image for component kube-controller-manager.
[upgrade/prepull] Prepulling image for component kube-scheduler.
[apiclient] Found 0 Pods for label selector k8s-app=upgrade-prepull-etcd
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-kube-controller-manager
[apiclient] Found 0 Pods for label selector k8s-app=upgrade-prepull-kube-scheduler
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-kube-apiserver
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-etcd
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-kube-scheduler
[upgrade/prepull] Prepulled image for component etcd.
[upgrade/prepull] Prepulled image for component kube-apiserver.
[upgrade/prepull] Prepulled image for component kube-controller-manager.
[upgrade/prepull] Prepulled image for component kube-scheduler.
[upgrade/prepull] Successfully prepulled the images for all the control plane components
[upgrade/apply] Upgrading your Static Pod-hosted control plane to version "v1.18.17"...
Static pod: kube-apiserver-amd64-02 hash: c09f9b33249bb59a2d1676078ff11e1d
Static pod: kube-controller-manager-amd64-02 hash: 37bc7b8265271b78f09bcff3665ac066
Static pod: kube-scheduler-amd64-02 hash: 36a66668027e3615a254b78961a85f6f
[upgrade/etcd] Upgrading to TLS for etcd
[upgrade/etcd] Non fatal issue encountered during upgrade: the desired etcd version for this Kubernetes version "v1.18.17" is "3.4.3-0", but the current etcd version is "3.4.3". Won't downgrade etcd, instead just continue
[upgrade/staticpods] Writing new Static Pod manifests to "/etc/kubernetes/tmp/kubeadm-upgraded-manifests372566520"
W0507 20:06:03.158301   35462 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[upgrade/staticpods] Preparing for "kube-apiserver" upgrade
[upgrade/staticpods] Renewing apiserver certificate
[upgrade/staticpods] Renewing apiserver-kubelet-client certificate
[upgrade/staticpods] Renewing front-proxy-client certificate
[upgrade/staticpods] Renewing apiserver-etcd-client certificate
[upgrade/staticpods] Moved new manifest to "/etc/kubernetes/manifests/kube-apiserver.yaml" and backed up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2021-05-07-20-06-01/kube-apiserver.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This might take a minute or longer depending on the component/version gap (timeout 5m0s)
Static pod: kube-apiserver-amd64-02 hash: c09f9b33249bb59a2d1676078ff11e1d
Static pod: kube-apiserver-amd64-02 hash: c09f9b33249bb59a2d1676078ff11e1d
Static pod: kube-apiserver-amd64-02 hash: c09f9b33249bb59a2d1676078ff11e1d
Static pod: kube-apiserver-amd64-02 hash: c09f9b33249bb59a2d1676078ff11e1d
Static pod: kube-apiserver-amd64-02 hash: c09f9b33249bb59a2d1676078ff11e1d
Static pod: kube-apiserver-amd64-02 hash: c09f9b33249bb59a2d1676078ff11e1d
Static pod: kube-apiserver-amd64-02 hash: 01177fcedc108bd4af215364f9326362
[apiclient] Found 1 Pods for label selector component=kube-apiserver
[upgrade/staticpods] Component "kube-apiserver" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-controller-manager" upgrade
[upgrade/staticpods] Renewing controller-manager.conf certificate
[upgrade/staticpods] Moved new manifest to "/etc/kubernetes/manifests/kube-controller-manager.yaml" and backed up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2021-05-07-20-06-01/kube-controller-manager.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This might take a minute or longer depending on the component/version gap (timeout 5m0s)
Static pod: kube-controller-manager-amd64-02 hash: 37bc7b8265271b78f09bcff3665ac066
Static pod: kube-controller-manager-amd64-02 hash: 018301583dcf0145dea334621262b391
[apiclient] Found 1 Pods for label selector component=kube-controller-manager
[upgrade/staticpods] Component "kube-controller-manager" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-scheduler" upgrade
[upgrade/staticpods] Renewing scheduler.conf certificate
[upgrade/staticpods] Moved new manifest to "/etc/kubernetes/manifests/kube-scheduler.yaml" and backed up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2021-05-07-20-06-01/kube-scheduler.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This might take a minute or longer depending on the component/version gap (timeout 5m0s)
Static pod: kube-scheduler-amd64-02 hash: 36a66668027e3615a254b78961a85f6f
Static pod: kube-scheduler-amd64-02 hash: 46d277871ac0ed187103437f98049236
[apiclient] Found 1 Pods for label selector component=kube-scheduler
[upgrade/staticpods] Component "kube-scheduler" upgraded successfully!
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.18" in namespace kube-system with the configuration for the kubelets in the cluster
[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.18" ConfigMap in the kube-system namespace
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

[upgrade/successful] SUCCESS! Your cluster was upgraded to "v1.18.17". Enjoy!

[upgrade/kubelet] Now that your control plane is upgraded, please proceed with upgrading your kubelets if you haven't already done so.
```

**dbuddenbaum@amd64-02:~$**
 
 sudo apt-get update
 
``` 
Hit:1 http://us.archive.ubuntu.com/ubuntu focal InRelease
Get:3 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:4 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Hit:5 https://download.newrelic.com/infrastructure_agent/linux/apt focal InRelease
Get:6 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]
Get:2 https://packages.cloud.google.com/apt kubernetes-xenial InRelease [9383 B]
Hit:7 http://packages.azlux.fr/debian buster InRelease
Get:8 http://us.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [955 kB]
Get:9 http://us.archive.ubuntu.com/ubuntu focal-updates/main i386 Packages [466 kB]
Err:2 https://packages.cloud.google.com/apt kubernetes-xenial InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
Get:10 http://us.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [768 kB]
Get:11 http://us.archive.ubuntu.com/ubuntu focal-updates/universe i386 Packages [567 kB]
Get:12 http://packages.cloud.google.com/apt kubernetes-xenial InRelease [9383 B]
Err:12 http://packages.cloud.google.com/apt kubernetes-xenial InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
Hit:13 https://download.docker.com/linux/ubuntu focal InRelease
Fetched 3098 kB in 10s (297 kB/s)
Reading package lists... Done
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://packages.cloud.google.com/apt kubernetes-xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://packages.cloud.google.com/apt kubernetes-xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu focal InRelease' doesn't support architecture 'i386'
W: Failed to fetch http://apt.kubernetes.io/dists/kubernetes-xenial/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Failed to fetch http://packages.cloud.google.com/apt/dists/kubernetes-xenial/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Some index files failed to download. They have been ignored, or old ones used instead.
```

**dbuddenbaum@amd64-02:~$**
 
 sudo apt-get install -y --allow-change-held-packages kubelet=1.18.17-00 kubectl=1.18.17-00
 
``` 
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following held packages will be changed:
  kubectl kubelet
The following packages will be upgraded:
  kubectl kubelet
2 upgraded, 0 newly installed, 0 to remove and 21 not upgraded.
Need to get 28.3 MB of archives.
After this operation, 2067 kB of additional disk space will be used.
Get:1 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubectl amd64 1.18.17-00 [8825 kB]
Get:2 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubelet amd64 1.18.17-00 [19.5 MB]
Fetched 28.3 MB in 14s (2076 kB/s)
(Reading database ... 144373 files and directories currently installed.)
Preparing to unpack .../kubectl_1.18.17-00_amd64.deb ...
Unpacking kubectl (1.18.17-00) over (1.17.11-00) ...
Preparing to unpack .../kubelet_1.18.17-00_amd64.deb ...
Unpacking kubelet (1.18.17-00) over (1.17.11-00) ...
Setting up kubectl (1.18.17-00) ...
Setting up kubelet (1.18.17-00) ...
```

dbuddenbaum@amd64-02:~$ sudo systemctl daemon-reload
dbuddenbaum@amd64-02:~$ sudo systemctl restart kubelet

**#( 05/07/21@ 4:17PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**

   kubectl uncordon amd64-02

```   
node/amd64-02 uncordoned
```

## Workers

**dbuddenbaum@amd64-06:~$** sudo apt-get update
```
Hit:1 http://us.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Hit:4 https://download.docker.com/linux/ubuntu focal InRelease
Get:5 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Get:6 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]
Get:7 http://us.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [955 kB]
Hit:3 https://packages.cloud.google.com/apt kubernetes-xenial InRelease
Hit:8 http://packages.azlux.fr/debian buster InRelease
Get:9 http://us.archive.ubuntu.com/ubuntu focal-updates/main i386 Packages [466 kB]
Get:10 http://us.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [768 kB]
Get:11 http://us.archive.ubuntu.com/ubuntu focal-updates/universe i386 Packages [567 kB]
Fetched 3079 kB in 2s (1753 kB/s)
Reading package lists... Done
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu focal InRelease' doesn't support architecture 'i386'
dbuddenbaum@amd64-06:~$ sudo apt-get install -y --allow-change-held-packages kubeadm=1.18.17-00
Reading package lists... Done
Building dependency tree
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 kubeadm : Depends: kubernetes-cni (>= 0.8.7)
E: Unable to correct problems, you have held broken packages.
```
**dbuddenbaum@amd64-06:~$** sudo apt-get install -y --allow-change-held-packages kubernetes-cni=0.8.7-00
```
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following held packages will be changed:
  kubernetes-cni
The following packages will be upgraded:
  kubernetes-cni
1 upgraded, 0 newly installed, 0 to remove and 53 not upgraded.
Need to get 25.0 MB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubernetes-cni amd64 0.8.7-00 [25.0 MB]
Fetched 25.0 MB in 12s (2147 kB/s)
(Reading database ... 144372 files and directories currently installed.)
Preparing to unpack .../kubernetes-cni_0.8.7-00_amd64.deb ...
Unpacking kubernetes-cni (0.8.7-00) over (0.8.6-00) ...
Setting up kubernetes-cni (0.8.7-00) ...
dbuddenbaum@amd64-06:~$ sudo apt-get install -y --allow-change-held-packages kubeadm=1.18.17-00
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following held packages will be changed:
  kubeadm
The following packages will be upgraded:
  kubeadm
1 upgraded, 0 newly installed, 0 to remove and 52 not upgraded.
Need to get 8168 kB of archives.
After this operation, 418 kB of additional disk space will be used.
Get:1 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubeadm amd64 1.18.17-00 [8168 kB]
Fetched 8168 kB in 4s (1826 kB/s)
(Reading database ... 144372 files and directories currently installed.)
Preparing to unpack .../kubeadm_1.18.17-00_amd64.deb ...
Unpacking kubeadm (1.18.17-00) over (1.17.11-00) ...
Setting up kubeadm (1.18.17-00) ...
```
**dbuddenbaum@amd64-06:~$** sudo kubeadm upgrade node
```
[upgrade] Reading configuration from the cluster...
[upgrade] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[upgrade] Skipping phase. Not a control plane node.
[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.18" ConfigMap in the kube-system namespace
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[upgrade] The configuration for this node was successfully updated!
[upgrade] Now you should go ahead and upgrade the kubelet package using your package manager.
```

**#( 05/07/21@ 4:39PM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   kubectl -n rook-ceph scale deployment rook-ceph-operator --replicas=0
   ```
deployment.apps/rook-ceph-operator scaled
```
**#( 05/07/21@ 4:55PM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   kubectl -n rook-ceph scale deployment rook-ceph-osd-7-75c759c84b-hdrf8 --replicas=0
   ```
Error from server (NotFound): deployments.apps "rook-ceph-osd-7-75c759c84b-hdrf8" not found
```
**#( 05/07/21@ 4:56PM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   kubectl -n rook-ceph scale deployment rook-ceph-osd-7 --replicas=0
   ```
deployment.apps/rook-ceph-osd-7 scaled
```
**#( 05/07/21@ 4:58PM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   kubectl -n rook-ceph scale deployment rook-ceph-osd-7 --replicas=1
   ```
deployment.apps/rook-ceph-osd-7 scaled
```
**#( 05/07/21@ 5:00PM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   kubectl -n rook-ceph scale deployment rook-ceph-osd-8 --replicas=0
   ```
deployment.apps/rook-ceph-osd-8 scaled
```
**#( 05/07/21@ 5:00PM )( dbuddenbaum@dbuddenbaum-mbp ):~**
   cd Documents/rPi4/kalaxy/yaml
**#( 05/07/21@ 5:02PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**
   cd rook-ceph/utils
**#( 05/07/21@ 5:02PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl create -f osd-purge.yaml
   ```
Error from server (AlreadyExists): error when creating "osd-purge.yaml": jobs.batch "rook-ceph-purge-osd" already exists
```
**#( 05/07/21@ 5:02PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl delete -f osd-purge.yaml
   ```
job.batch "rook-ceph-purge-osd" deleted
```
**#( 05/07/21@ 5:03PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl create -f osd-purge.yaml
   ```
job.batch/rook-ceph-purge-osd created
```
**#( 05/07/21@ 5:03PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl -n rook-ceph logs -l app=rook-ceph-purge-osd
**#( 05/07/21@ 5:06PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl -n rook-ceph logs -l app=rook-ceph-purge-osd
**#( 05/07/21@ 5:06PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl delete -f osd-purge.yaml
   ```
job.batch "rook-ceph-purge-osd" deleted
```
**#( 05/07/21@ 5:07PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl delete deployment -n rook-ceph rook-ceph-osd-8
   ```
Error from server (NotFound): deployments.apps "rook-ceph-osd-8" not found
```

**#( 05/07/21@ 5:17PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl drain amd64-06 --ignore-daemonsets
   ```
node/amd64-06 cordoned
evicting pod "rook-ceph-crashcollector-amd64-06-56bcd6f554-wqbsv"
evicting pod "rook-ceph-osd-prepare-amd64-06-mb8v4"
pod/rook-ceph-osd-prepare-amd64-06-mb8v4 evicted
pod/rook-ceph-crashcollector-amd64-06-56bcd6f554-wqbsv evicted
node/amd64-06 evicted
```

**dbuddenbaum@amd64-06:~$** sudo apt-get update
```
Hit:1 http://us.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Hit:4 https://download.docker.com/linux/ubuntu focal InRelease
Get:5 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]
Get:6 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Hit:7 http://packages.azlux.fr/debian buster InRelease
Hit:3 https://packages.cloud.google.com/apt kubernetes-xenial InRelease
Fetched 324 kB in 1s (292 kB/s)
Reading package lists... Done
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu focal InRelease' doesn't support architecture 'i386'
dbuddenbaum@amd64-06:~$ sudo apt-get install -y --allow-change-held-packages kubelet=1.18.17-00 kubectl=1.18.17-00
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following held packages will be changed:
  kubectl kubelet
The following packages will be upgraded:
  kubectl kubelet
2 upgraded, 0 newly installed, 0 to remove and 51 not upgraded.
Need to get 28.3 MB of archives.
After this operation, 2067 kB of additional disk space will be used.
Get:1 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubectl amd64 1.18.17-00 [8825 kB]
Get:2 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubelet amd64 1.18.17-00 [19.5 MB]
Fetched 28.3 MB in 13s (2109 kB/s)
(Reading database ... 144372 files and directories currently installed.)
Preparing to unpack .../kubectl_1.18.17-00_amd64.deb ...
Unpacking kubectl (1.18.17-00) over (1.17.11-00) ...
Preparing to unpack .../kubelet_1.18.17-00_amd64.deb ...
Unpacking kubelet (1.18.17-00) over (1.17.11-00) ...
Setting up kubectl (1.18.17-00) ...
Setting up kubelet (1.18.17-00) ...
```
**dbuddenbaum@amd64-06:~$** sudo systemctl daemon-reload

**dbuddenbaum@amd64-06:~$** sudo systemctl restart kubelet

**#( 05/07/21@ 5:25PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/rook-ceph/utils@master✗✗✗**
   kubectl uncordon amd64-06
   ```
node/amd64-06 uncordoned
```