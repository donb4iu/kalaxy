# Monitoring 1-5

- [Building an ARM Kubernetes Cluster](https://itnext.io/building-an-arm-kubernetes-cluster-ef31032636f9)
- [Building a hybrid x86–64 and ARM Kubernetes Cluster](https://medium.com/@carlosedp/building-a-hybrid-x86-64-and-arm-kubernetes-cluster-e7f94ff6e51d)
- [Deploying multiple Traefik Ingresses with LetsEncrypt HTTPS certificates on Kubernetes](https://medium.com/@carlosedp/multiple-traefik-ingresses-with-letsencrypt-https-certificates-on-kubernetes-b590550280cf)
- [Install a Kubernetes load balancer on your Raspberry Pi homelab with MetalLB](https://opensource.com/article/20/7/homelab-metallb?utm_campaign=intrel)
- [Using MetalLB And Traefik Load Balancing For Your Bare Metal Kubernetes Cluster – Part 1](https://www.devtech101.com/2019/02/23/using-metallb-and-traefik-load-balancing-for-your-bare-metal-kubernetes-cluster-part-1/)
- [Kubernetes Metal LB for On-Prem / BareMetal Cluster in 10 minutes](https://medium.com/@JockDaRock/kubernetes-metal-lb-for-on-prem-baremetal-cluster-in-10-minutes-c2eaeb3fe813)

## traefik and metallb
https://github.com/kubernetes-retired/external-storage/blob/master/nfs-client/deploy/deployment-arm.yaml
https://github.com/kubernetes-sigs/sig-storage-lib-external-provisioner

https://github.com/carlosedp/kubernetes-arm/

[Building a hybrid x86–64 and ARM Kubernetes Cluster](https://medium.com/@carlosedp/building-a-hybrid-x86-64-and-arm-kubernetes-cluster-e7f94ff6e51d)


To allow Jobs to use the TTL feature, edit all manifests using sudo in the Master Node from /etc/kubernetes/manifests and add the flag — --feature-gates=TTLAfterFinished=true below to the start end of the command section:
```
...
spec:
  containers:
  - command:
    - kube-apiserver
    - --authorization-mode=Node,RBAC
...
- --feature-gates=TTLAfterFinished=true
```

remove host so all traffic [Deploying Traefik as Ingress Controller for Your Kubernetes Cluster:An optional host](https://medium.com/kubernetes-tutorials/deploying-traefik-as-ingress-controller-for-your-kubernetes-cluster-b03a0672ae0c)

**#( 11/11/20@12:57AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**
   kubectl create ns metallb-system
```
namespace/metallb-system created
```
**#( 11/11/20@ 1:01AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**
   kubectl apply -f ./1-MetalLB/metallb-conf.yaml
```   
configmap/config created
```

**#( 11/24/20@ 1:51AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/1-MetalLB@master✗✗✗**

   helm install metallb --namespace=metallb-system -f metallb-conf.yaml stable/metallb

```
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: This chart is deprecated
NAME: metallb
LAST DEPLOYED: Tue Nov 24 01:51:59 2020
NAMESPACE: metallb-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
############################################################
####          WARNING: This chart is deprecated         ####
############################################################

MetalLB is now running in the cluster.
WARNING: you specified a ConfigMap that isn't managed by
Helm. LoadBalancer services will not function until you add that
ConfigMap to your cluster yourself.

```


**#( 11/11/20@ 1:01AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**
   cd 2-Traefik

**#( 11/11/20@ 1:21AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/2-Traefik@master✗✗✗**
   ./deploy
```
clusterrole.rbac.authorization.k8s.io/traefik-ingress-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/traefik-ingress-controller unchanged
configmap/traefik-conf created
service/traefik-ingress-service created
ingress.extensions/traefik-ingress-lb created
serviceaccount/traefik-ingress-controller unchanged
deployment.apps/traefik-ingress-controller created
```
**#( 11/11/20@ 2:16AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/3-NFS_Storage@master✗✗✗**
   ./deploy
```
namespace/nfs-storage created
serviceaccount/nfs-client-provisioner created
clusterrole.rbac.authorization.k8s.io/nfs-client-provisioner-runner created
clusterrolebinding.rbac.authorization.k8s.io/run-nfs-client-provisioner created
role.rbac.authorization.k8s.io/leader-locking-nfs-client-provisioner created
rolebinding.rbac.authorization.k8s.io/leader-locking-nfs-client-provisioner created
deployment.apps/nfs-client-provisioner created
storageclass.storage.k8s.io/nfs-ssd1 created
storageclass.storage.k8s.io/nfs-ssd1 patched (no change)
deployment.apps/nfs-client-provisioner patched
```