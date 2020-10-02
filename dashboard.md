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
Name:		admin-user-token-tsrds
Namespace:	kubernetes-dashboard
Labels:		<none>
Annotations:	kubernetes.io/service-account.name=admin-user
		kubernetes.io/service-account.uid=1ddca997-6f22-4fc4-86d4-cd6b794b20e3

Type:	kubernetes.io/service-account-token

Data
====
token:		eyJhbGciOiJSUzI1NiIsImtpZCI6IlEyWUF6VzllSEExeldZUmFBRDU5VzNRNXlVbURzb1dueENER09KUTFFSzgifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLXRzcmRzIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIxZGRjYTk5Ny02ZjIyLTRmYzQtODZkNC1jZDZiNzk0YjIwZTMiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.iYX9F-JyK9ssh8TjE3C-pMuWWOjHkuFR-vP5lJmBkJP5e1arVaQ4UNEyacKIc6yXrKKh3e0rFgVLGlF9TgoHk_uA366fR0OQ-23Uqap5ZTuL_ZIR_uoFmOwk_BawFAupTzErKDT3Vl96wOaf4OzILGCzI0Avadsp2mdEYaahKhuuX1bPy-KM04wHFNr5U8OpCRDQOfXGdv6xU5NBZqG9uwlrR5hemWP8lwFkc-GS3Gzi3KcIM0rWv7shodR_pn1uMf-wLR1y8lwZ1RhSdh2pmImaqepWr9Uvf6vl4mfW752nTHahvFfsFWSVE2st0zlxQjJSNbWCBzdi9KTu747KfQ
ca.crt:		1025 bytes
namespace:	20 bytes
```