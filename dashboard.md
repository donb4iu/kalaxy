# Dashboard

![kubernetesdashboard](images/dashboard.png)


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
Name:         admin-user-token-qw58q
Namespace:    kubernetes-dashboard
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 75135668-12ae-4643-a28d-03c97f91e2ca

Type:  kubernetes.io/service-account-token

Data
====
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImstVk1XSWdsMXlLTWNyYzhncmY4SzU3WkVpYWVpZnRiTW96UGlUUHlmMHcifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLXF3NThxIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI3NTEzNTY2OC0xMmFlLTQ2NDMtYTI4ZC0wM2M5N2Y5MWUyY2EiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.bs0dauGds6qHN483QYJhY9UHg7l4dJel0WPBQ-KExfO2BCLBZul5MIk1Y-6cycYJoEj9ZWp1zBjBzktIWtG82cO54anWORuQ1RC6AeeBb_jiBTak89ItUCAztZyobWPaD3wVD6A9w2nL6RjsxzrAlDLyCQiH7yww5Z1ICnKHI9kVkMWq9j1Tcu4udXPYFkPQ4BFfNxgZ0L8nx7GoHLVBZ5IY3Jv81sAeCX5_z0T6dXJwPHUfdDOUCYbU9lz8-J4YEZJohJdGmoFMdNMR5bX-ns_v7S04BVmdFdryVJdq1z85imbNEDIztHkkmeLUVOPy9KCoCwP3tJyiS2VRcYDFjg
ca.crt:     1025 bytes
namespace:  20 bytes
```

[Kubernetes Dashboard Adjusting the timeout of the Kubernetes Dashboard](https://blinkeye.github.io/post/public/2019-05-30-kubernetes-dashboard/)

![kubernetes-dashboard-ttl.png](images/kubernetes-dashboard-ttl.png)
![kubernetes-dashboard-args.png](images/kubernetes-dashboard-args.png)