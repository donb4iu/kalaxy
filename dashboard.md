# Dashboard

![kubernetesdashboard](images/dashboard.png)
[Kubernetes Dashboard](https://github.com/kubernetes/dashboard)

## [Dashboard](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)

**kubectl apply --filename https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta4/aio/deploy/recommended.yaml**

**[18:39:42]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy$** kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-rc7/aio/deploy/recommended.yaml --validate=false
```
namespace "kubernetes-dashboard" created
serviceaccount "kubernetes-dashboard" created
service "kubernetes-dashboard" created
secret "kubernetes-dashboard-certs" created
secret "kubernetes-dashboard-csrf" created
secret "kubernetes-dashboard-key-holder" created
configmap "kubernetes-dashboard-settings" created
role "kubernetes-dashboard" created
clusterrole "kubernetes-dashboard" created
rolebinding "kubernetes-dashboard" created
clusterrolebinding "kubernetes-dashboard" created
deployment "kubernetes-dashboard" created
service "dashboard-metrics-scraper" created
deployment "dashboard-metrics-scraper" created
```

**[18:48:28]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy$** kubectl apply -f CreatingaServiceAccount.yaml --validate=false
   ```
serviceaccount "admin-user" created
```
**[18:48:46]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy$** kubectl apply -f CreatingaClusterRoleBinding.yaml --validate=false
```
clusterrolebinding "admin-user" configured
```

**#( 10/24/20@ 4:13PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml@master✗✗✗**  kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```
Name:         admin-user-token-p28gh
Namespace:    kube-system
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 40fb41c7-8314-4eec-8128-0d69089a4ad2

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1025 bytes
namespace:  11 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImstVk1XSWdsMXlLTWNyYzhncmY4SzU3WkVpYWVpZnRiTW96UGlUUHlmMHcifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLWc0Mm5zIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI4Mzc2YzI1Ni1kOTIxLTQ4NDgtOTQwNC1hZGNhYTgyMWJkMWIiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06YWRtaW4tdXNlciJ9.xYK9ZQnLSabsZPvafWXEdsXDfP4pFSWS_tJyj4m04akWdFTPVcfYkfjpvIJG1qVW1k9QuRqrNAhKCHASCePkusv7yWoOaflzO5FlEQfj_bPjD95HZNs3rDGNmMu0iTxDzV34UqrGXtmPKNuiXIjZFWIQfdiadXGOm7FoPpH-X0JAvavutHEoifSa9KK1RM4h3ko1N2UzU5tGGTUZQrYlgmcpoUYMRy7NWk1hwKNxCSm9S7QDLnC7RUKi0R0tKj4Zf8ZT_tRZpi7uCxgi9NYRmHv7RUoyAQCEftaNicNio-MgvA9QvDLsskYfe0oSede8bZePrCcgtQdqoAR2X02yMQ
```

[Kubernetes Dashboard Adjusting the timeout of the Kubernetes Dashboard](https://blinkeye.github.io/post/public/2019-05-30-kubernetes-dashboard/)

![kubernetes-dashboard-ttl.png](images/kubernetes-dashboard-ttl.png)
![kubernetes-dashboard-args.png](images/kubernetes-dashboard-args.png)

## dashboard -4
* [Configuring HA Kubernetes cluster on bare metal servers, monitoring, logs, and usage examples. 3/3](https://medium.com/faun/configuring-ha-kubernetes-cluster-on-bare-metal-servers-monitoring-logs-and-usage-examples-3-3-340357f21453)

* [Building a hybrid x86–64 and ARM Kubernetes Cluster](https://carlosedp.medium.com/building-a-hybrid-x86-64-and-arm-kubernetes-cluster-e7f94ff6e51d)

**#( 12/11/20@ 1:53AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/4-Dashboard@master✗✗✗**
   
   kubectl create -f dashboard.yaml
```
secret/kubernetes-dashboard-certs created
serviceaccount/kubernetes-dashboard created
role.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
deployment.apps/kubernetes-dashboard created
service/kubernetes-dashboard created
```
**#( 12/11/20@ 1:54AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/4-Dashboard@master✗✗✗**
  
   kubectl get svc --namespace=kube-system
```
NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                                     AGE
kube-dns                  ClusterIP      10.96.0.10       <none>         53/UDP,53/TCP,9153/TCP                      46d
kubernetes-dashboard      LoadBalancer   10.107.145.32    192.168.2.12   443:30135/TCP                               70s
metrics-server            ClusterIP      10.100.14.34     <none>         443/TCP                                     24d
traefik-ingress-service   LoadBalancer   10.106.124.204   192.168.2.20   80:32538/TCP,443:31837/TCP,8080:30359/TCP   16d
```
**#( 12/11/20@ 2:19AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/4-Dashboard@master✗✗✗**
   
   kubectl create -f dashboard-admin-account.yaml
```
serviceaccount/admin-user created
clusterrolebinding.rbac.authorization.k8s.io/admin-user created
```
**#( 12/11/20@ 2:19AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/4-Dashboard@master✗✗✗**
  
   kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```
Name:         admin-user-token-g42ns
Namespace:    kube-system
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 8376c256-d921-4848-9404-adcaa821bd1b

Type:  kubernetes.io/service-account-token

Data
====
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImstVk1XSWdsMXlLTWNyYzhncmY4SzU3WkVpYWVpZnRiTW96UGlUUHlmMHcifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLWc0Mm5zIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI4Mzc2YzI1Ni1kOTIxLTQ4NDgtOTQwNC1hZGNhYTgyMWJkMWIiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06YWRtaW4tdXNlciJ9.xYK9ZQnLSabsZPvafWXEdsXDfP4pFSWS_tJyj4m04akWdFTPVcfYkfjpvIJG1qVW1k9QuRqrNAhKCHASCePkusv7yWoOaflzO5FlEQfj_bPjD95HZNs3rDGNmMu0iTxDzV34UqrGXtmPKNuiXIjZFWIQfdiadXGOm7FoPpH-X0JAvavutHEoifSa9KK1RM4h3ko1N2UzU5tGGTUZQrYlgmcpoUYMRy7NWk1hwKNxCSm9S7QDLnC7RUKi0R0tKj4Zf8ZT_tRZpi7uCxgi9NYRmHv7RUoyAQCEftaNicNio-MgvA9QvDLsskYfe0oSede8bZePrCcgtQdqoAR2X02yMQ
ca.crt:     1025 bytes
namespace:  11 bytes

```

**#( 12/11/20@ 2:19AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/4-Dashboard@master✗✗✗**

kubectl create -f metrics-scrapper.yaml



## reference
 
- [Expose your Kubernetes Dashboard using a LoadBalancer](https://github.com/alexandreroman/k8s-dashboard-loadbalancer)
- [Bare metal load balancer on Kubernetes with MetalLB ](https://dev.to/drazisil/bare-metal-load-balancer-on-kubernetes-with-metallb-3h2k)
- [TKS (TJ's Kubernetes Service)](https://github.com/zimmertr/Bootstrap-Kubernetes-with-QEMU/blob/master/playbooks/optional/deploy_dashboard.yml)

- [https://github.com/kubernetes/dashboard/blob/master/docs/user/accessing-dashboard/README.md](https://github.com/kubernetes/dashboard/blob/master/docs/user/accessing-dashboard/README.md)
- [https://gist.github.com/addshore/5e1fbfeb3bd97f8ebf50d68899c28fd5](https://gist.github.com/addshore/5e1fbfeb3bd97f8ebf50d68899c28fd5)


- [https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca](https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca)


- [The Ultimate Guide to the Kubernetes Dashboard: How to Install and Integrate Metrics-server](https://www.replex.io/blog/the-ultimate-guide-to-the-kubernetes-dashboard-how-to-install-and-integrate-metrics-server)