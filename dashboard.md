# Dashboard

![kubernetesdashboard](images/dashboard.png)
[Kubernetes Dashboard](https://github.com/kubernetes/dashboard)

## [Dashboard](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)

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
Name:         admin-user-token-5vf6v
Namespace:    kubernetes-dashboard
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 000195ce-772f-4a5b-85d7-2afdddfe7bb7

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1025 bytes
namespace:  20 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImstVk1XSWdsMXlLTWNyYzhncmY4SzU3WkVpYWVpZnRiTW96UGlUUHlmMHcifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLTV2ZjZ2Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIwMDAxOTVjZS03NzJmLTRhNWItODVkNy0yYWZkZGRmZTdiYjciLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.RdMzhkLOff7bm2ssZ9Grcg0r8SJlRUhD50LZNr2WUUK0wByNleBP5163Jiy7Gc5P11inObt2PPpdMRClUr_q7qY-Ua2gts4VU-7CZajaimye01mPO_PJgLTKy7ov3H9OqFdWDnqYCHV2ivfI9Y51D8OJL5jR8seDkfC11H1_DLwiutzKWVvHlRkq7AGU47QhIJAxqKQxpdyp3oJn0r-MdvNttN8jXAnKzeZMnURv1GEdxI5XG6eilQ_zt-DGLAAIyEqXAfR9DmUa7voUiTmqAvH-v952eJS-P78Pu2MxaYfa05mQMHGOTNkXkl8Bd70u_hLzYoHcKETdwSlw5iyrrw
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
Name:         admin-user-token-25lkc
Namespace:    kube-system
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 2439f9cb-658e-4841-92f8-57467ce23bf8

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1025 bytes
namespace:  11 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImstVk1XSWdsMXlLTWNyYzhncmY4SzU3WkVpYWVpZnRiTW96UGlUUHlmMHcifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLTI1bGtjIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIyNDM5ZjljYi02NThlLTQ4NDEtOTJmOC01NzQ2N2NlMjNiZjgiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06YWRtaW4tdXNlciJ9.b6OLgFnl4qxYz0ScDvO_-65bj80oH6_4HnLHD9y6IS2mzVCIaaMcPgltbzuhEoxX1Udnj5hMNeRXA6mcfkliIsWfh8Kk8MdIazbYxuaeNJAlzHga1ki6kkQBIBAJQ9HJ0ZMZrkx6WQsHy5PpOb-Rm_hInGjKc-fmE6jTC1egM6MBtBhgCxUJrcgkZdnsE1uX-tTHTEGQhHezJ6lNs6HolaONN4CiM4v6IViAqSaLCDX4FUEarzOdEzBur8fWedkX0QVcM1mIbT2z7nm6pKNik9bcIB1GvIUz7w1Zd6Aoh6sZ3owYW66tgH4XpcVCNApxhEx3NWXGuHTZwBehSUtg3w```
```


## reference
[Expose your Kubernetes Dashboard using a LoadBalancer](https://github.com/alexandreroman/k8s-dashboard-loadbalancer)
[Bare metal load balancer on Kubernetes with MetalLB ](https://dev.to/drazisil/bare-metal-load-balancer-on-kubernetes-with-metallb-3h2k)
[TKS (TJ's Kubernetes Service)](https://github.com/zimmertr/Bootstrap-Kubernetes-with-QEMU/blob/master/playbooks/optional/deploy_dashboard.yml)

[https://github.com/kubernetes/dashboard/blob/master/docs/user/accessing-dashboard/README.md](https://github.com/kubernetes/dashboard/blob/master/docs/user/accessing-dashboard/README.md)
[https://gist.github.com/addshore/5e1fbfeb3bd97f8ebf50d68899c28fd5](https://gist.github.com/addshore/5e1fbfeb3bd97f8ebf50d68899c28fd5)


[https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca](https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca
)


#( 12/04/20@ 4:03AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4
   openssl req -nodes -newkey rsa:2048 -keyout certs/dashboard.key -out certs/dashboard.csr -subj "/C=/ST=/L=/O=/OU=/CN=kubernetes-dashboard"
Generating a 2048 bit RSA private key
................................................+++
..................................................................................................................+++
writing new private key to 'certs/dashboard.key'
-----
No value provided for Subject Attribute C, skipped
No value provided for Subject Attribute ST, skipped
No value provided for Subject Attribute L, skipped
No value provided for Subject Attribute O, skipped
No value provided for Subject Attribute OU, skipped
#( 12/04/20@ 4:03AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4
   openssl x509 -req -sha256 -days 365 -in certs/dashboard.csr -signkey certs/dashboard.key -out certs/dashboard.crt
Signature ok
subject=/CN=kubernetes-dashboard
Getting Private key
#( 12/04/20@ 4:03AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4
   cd certs
#( 12/04/20@ 4:04AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/certs
   ls -la
total 24
drwxr-xr-x   5 dbuddenbaum  staff   160 Dec  4 04:03 .
drwxr-xr-x  15 dbuddenbaum  staff   480 Dec  4 04:01 ..
-rw-r--r--   1 dbuddenbaum  staff  1005 Dec  4 04:03 dashboard.crt
-rw-r--r--   1 dbuddenbaum  staff   907 Dec  4 04:03 dashboard.csr
-rw-r--r--   1 dbuddenbaum  staff  1704 Dec  4 04:03 dashboard.key
#( 12/04/20@ 4:05AM )( dbuddenbaum@dbuddenbaum-mbp ):~
   kubectl delete secret generic kubernetes-dashboard-certs  -n kubernetes-dashboard
cd ..
secret "kubernetes-dashboard-certs" deleted
Error from server (NotFound): secrets "generic" not found
#( 12/04/20@ 4:07AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/certs
   kubectl create secret generic kubernetes-dashboard-certs --from-file=dashboard.crt -n kubernetes-dashboard
secret/kubernetes-dashboard-certs created
#( 12/04/20@ 4:08AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/certs
   kubectl delete pod -n kubernetes-dashboard -l k8s-app=kubernetes-dashboard

pod "kubernetes-dashboard-64999dbccd-6pdlc" deleted
#( 12/04/20@ 4:09AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/certs
