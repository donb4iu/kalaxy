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

**[18:48:55]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy$** kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```
Name:         admin-user-token-vsrjb
Namespace:    kubernetes-dashboard
Labels:       <none>
Annotations:  kubernetes.io/service-account.name=admin-user
              kubernetes.io/service-account.uid=c572d182-7ca3-4d19-800e-6a254d11f111

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1025 bytes
namespace:  20 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IjBncmotRkpOVE1VMHRhSE4yMjU2MXNBaXlLZHdzek93VDdsd01OZDdoUDAifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLXZzcmpiIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiJjNTcyZDE4Mi03Y2EzLTRkMTktODAwZS02YTI1NGQxMWYxMTEiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.vbZg5k4UXfgjJuaJwLyCq9xyT3J2tyHtV7Dh0N2rJQCSIgXlb3bm3jNDeTbfHE0z9MCCrycP20yT4NkGZZWrdSUSTJKJzRq-cK0drEBHuR0QAv_ywhUB3BXhLXnp5yKwWsRaW99SdtQm6EWX8HcveQ1uBTdK-kcFXLb8C4zbijJIpHHAGbQpipzxPwF9vDTsaepQzYyfxzYbKxHvSw83a4uDu7XT0FNSOqwgXc1orq95-pd93qeTWUukDxybvTeIT6vqIdIF9bWIXbfwLz7SSyPQNU6MTfHNPrWJwajfM4CBuDy-H7VjpEenvRa-c1kEiP1s_gtqqX_Jwhlrnj0p2A
```