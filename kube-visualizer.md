# Kube Vusualizer

[https://schoolofdevops.github.io/ultimate-kubernetes-bootcamp/kube_visualizer/](https://schoolofdevops.github.io/ultimate-kubernetes-bootcamp/kube_visualizer/)



**#( 11/22/20@ 7:22PM )( dbuddenbaum@dbuddenbaum-mbp ):~**

   cd Documents/rPi4/kalaxy/yaml

**#( 11/22/20@ 7:22PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**

   kubectl apply -f kube-visualizer/
```
serviceaccount/kube-ops-view unchanged
clusterrole.rbac.authorization.k8s.io/kube-ops-view unchanged
clusterrolebinding.rbac.authorization.k8s.io/kube-ops-view unchanged
deployment.apps/kube-ops-view created
ingress.extensions/kube-ops-view unchanged
service/kube-ops-view created
```
**#( 11/22/20@ 7:23PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**
   
   kubectl get svc
```
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kube-ops-view   NodePort    10.101.194.65   <none>        80:32000/TCP   14s
```