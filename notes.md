# Installation Notes

## Raspberry Pi Monitoring

```
sudo apt-get update && sudo apt-get install htop -y
```

## make up
```
xcode-select --install
```
## Flash

```bash
flash \
    --userdata setup/cloud-config.yml \
    ~/Downloads/ubuntu-20.04-preinstalled-server-arm64+raspi.img
```
## [Dashboard](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)


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
Name:		admin-user-token-hv54n
Namespace:	kubernetes-dashboard
Labels:		<none>
Annotations:	kubernetes.io/service-account.name=admin-user
		kubernetes.io/service-account.uid=926ec66d-5733-4c74-8ddf-592cb6b70007

Type:	kubernetes.io/service-account-token

Data
====
ca.crt:		1025 bytes
namespace:	20 bytes
token:		eyJhbGciOiJSUzI1NiIsImtpZCI6IkpSVm1oNGZHNXZfRHNWYWZ3aXFTeWZyZUJjaWhHcXV5amdwV1VlcmJTbncifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLWh2NTRuIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI5MjZlYzY2ZC01NzMzLTRjNzQtOGRkZi01OTJjYjZiNzAwMDciLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.gNGfajnsjKuv0IolteUZBnfr9Kk53gap7sT-_t-p3bwu3pILlOpRHHZbVX0-qyR0omLcEzSPSy21EUOu3CNKkapMpuiiWeXE4tceCAvwXck2p1A6k-jbA-g7yh5f--NeaamvKlhjm7v26IKSBfF6W8SWXLOXg_dQHtI7Xyaf9bmfjNoB-kz5jMRDt_8jzmlHytVrS5xrcwD6-ntdW_E6QELLRf9Ze8tOGxFv9qq8pnHwKSCdsfSMr6evA0AL7yraaxNgN0VcQKzuetenQVSzR4Avm3nsvyuie9j-q0IODD8_H0rz-dW1qLrm82Eva9xDQy-PNF0JgihUrfVgBuqB_A```
```