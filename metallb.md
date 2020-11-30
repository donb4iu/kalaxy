# metallb installation / configuration

[Kubernetes Metal LB for On-Prem / BareMetal Cluster in 10 minutes](https://medium.com/@JockDaRock/kubernetes-metal-lb-for-on-prem-baremetal-cluster-in-10-minutes-c2eaeb3fe813)

## Setup

**#( 11/26/20@ 3:52AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/1-MetalLB@master✗✗✗**

   kubectl create -f https://raw.githubusercontent.com/google/metallb/v0.8.1/manifests/metallb.yaml
   
```   
namespace/metallb-system created
podsecuritypolicy.policy/speaker created
serviceaccount/controller created
serviceaccount/speaker created
clusterrole.rbac.authorization.k8s.io/metallb-system:controller created
clusterrole.rbac.authorization.k8s.io/metallb-system:speaker created
role.rbac.authorization.k8s.io/config-watcher created
clusterrolebinding.rbac.authorization.k8s.io/metallb-system:controller created
clusterrolebinding.rbac.authorization.k8s.io/metallb-system:speaker created
rolebinding.rbac.authorization.k8s.io/config-watcher created
daemonset.apps/speaker created
deployment.apps/controller created
```

**#( 11/26/20@ 2:52AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/1-MetalLB@master✗✗✗**0
 
   kubectl apply -f nginxlb.yaml

```
deployment.apps/nginx created
service/nginx unchanged
```
