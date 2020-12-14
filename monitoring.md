# Monitoring

[Monitoring and Alerting on your Kubernetes Cluster with Prometheus and Grafana](https://gregoiredayet.medium.com/monitoring-and-alerting-on-your-kubernetes-cluster-with-prometheus-and-grafana-55e4b427b22d)

## Prometheus
helm repo add stable https://kubernetes-charts.storage.googleapis.com
helm repo list

```WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
   WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
   NAME  	URL
   stable	https://kubernetes-charts.storage.googleapis.com```

```
## prometheus-kube
https://github.com/youngkin/prometheus-kube
[kubernetes-application-monitoring-on-a-raspberry-pi-cluster](https://medium.com/better-programming/kubernetes-application-monitoring-on-a-raspberry-pi-cluster-fa8f2762b00c)

[nodeSelector: {
       kubernetes.io/arch: arm64
}](https://github.com/youngkin/prometheus-kube/blob/master/helm/prometheus/values.yaml)


**#( 11/09/20@11:19PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/prometheus-kube@master✗✗✗**

   kubectl create ns monitor
```
namespace/monitor created
```
**#( 11/09/20@11:27PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/prometheus-kube@master✗✗✗**
   helm install --namespace monitor prometheus helm/prometheus
```  
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
NAME: prometheus
LAST DEPLOYED: Mon Nov  9 23:27:26 2020
NAMESPACE: monitor
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. Get the application URL by running these commands:
  http://prom.kube/
```
## prometheus-operator
https://github.com/youngkin/charts/tree/master/stable/prometheus-operator
[monitor-your-kubernetes-cluster-with-prometheus-and-grafana](https://medium.com/better-programming/monitor-your-kubernetes-cluster-with-prometheus-and-grafana-1f7d0195e59)

**#( 11/09/20@10:17PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4**
   kubectl create ns monitor
```
namespace/monitor created
```
**#( 11/09/20@10:17PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4**
   helm install prometheus stable/prometheus-operator --namespace monitor --set \
 nodeSelector."kubernetes\\.in/arch"=amd64
```
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: This chart is deprecated
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: prometheus
LAST DEPLOYED: Mon Nov  9 22:17:52 2020
NAMESPACE: monitor
STATUS: deployed
REVISION: 1
NOTES:
*******************
*** DEPRECATED ****
*******************
* stable/prometheus-operator chart is deprecated.
* Further development has moved to https://github.com/prometheus-community/helm-charts
* The chart has been renamed kube-prometheus-stack to more clearly reflect
* that it installs the `kube-prometheus` project stack, within which Prometheus
* Operator is only one component.

The Prometheus Operator has been installed. Check its status by running:
  kubectl --namespace monitor get pods -l "release=prometheus"

Visit https://github.com/coreos/prometheus-operator for instructions on how
to create & configure Alertmanager and Prometheus instances using the Operator.
```
**#( 11/09/20@10:19PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4**
    **kubectl --namespace monitor get pods -l "release=prometheus"**
```
NAME                                                   READY   STATUS             RESTARTS   AGE
prometheus-prometheus-node-exporter-8bbb2              1/1     Running            0          98s
prometheus-prometheus-node-exporter-fdfhg              1/1     Running            0          98s
prometheus-prometheus-node-exporter-js2jk              1/1     Running            0          98s
prometheus-prometheus-node-exporter-jsrrh              1/1     Running            0          98s
prometheus-prometheus-node-exporter-rd72x              1/1     Running            0          98s
prometheus-prometheus-node-exporter-rtwk9              1/1     Running            0          98s
prometheus-prometheus-node-exporter-s8cdb              1/1     Running            0          98s
prometheus-prometheus-node-exporter-t66hz              1/1     Running            0          98s
prometheus-prometheus-node-exporter-xbhvk              1/1     Running            0          98s
prometheus-prometheus-oper-operator-85cc758cdb-hjwdt   0/2     CrashLoopBackOff   4          98s

```

## Cluster Monitoring stack for ARM / X86-64 platforms

https://github.com/youngkin/cluster-monitoring

[https://github.com/youngkin/cluster-monitoring](https://github.com/youngkin/cluster-monitoring)

[Building a hybrid x86–64 and ARM Kubernetes Cluster](https://medium.com/@carlosedp/building-a-hybrid-x86-64-and-arm-kubernetes-cluster-e7f94ff6e51d)