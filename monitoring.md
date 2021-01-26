# Monitoring
[Practical Monitoring with Prometheus & Grafana (Part I)](https://yitaek.medium.com/practical-monitoring-with-prometheus-grafana-part-i-22d0f172f993)
[Monitoring and Alerting on your Kubernetes Cluster with Prometheus and Grafana](https://gregoiredayet.medium.com/monitoring-and-alerting-on-your-kubernetes-cluster-with-prometheus-and-grafana-55e4b427b22d)

## Prometheus (new location https://charts.helm.sh/stable)
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
   
   kubectl --namespace monitor get pods -l "release=prometheus"
   
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


helm install grafana stable/grafana

## Cluster Monitoring stack for ARM / X86-64 platforms

https://github.com/youngkin/cluster-monitoring

[https://github.com/youngkin/cluster-monitoring](https://github.com/youngkin/cluster-monitoring)

[Building a hybrid x86–64 and ARM Kubernetes Cluster](https://medium.com/@carlosedp/building-a-hybrid-x86-64-and-arm-kubernetes-cluster-e7f94ff6e51d)

**#( 12/21/20@ 9:15PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4**
  
   helm install prometheus stablenew/prometheus -n monitor

```   
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: This chart is deprecated
NAME: prometheus
LAST DEPLOYED: Mon Dec 21 21:16:17 2020
NAMESPACE: monitor
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
DEPRECATED and moved to <https://github.com/prometheus-community/helm-charts>The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
prometheus-server.monitor.svc.cluster.local


Get the Prometheus server URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace monitor -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace monitor port-forward $POD_NAME 9090


The Prometheus alertmanager can be accessed via port 80 on the following DNS name from within your cluster:
prometheus-alertmanager.monitor.svc.cluster.local


Get the Alertmanager URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace monitor -l "app=prometheus,component=alertmanager" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace monitor port-forward $POD_NAME 9093
#################################################################################
######   WARNING: Pod Security Policy has been moved to a global property.  #####
######            use .Values.podSecurityPolicy.enabled with pod-based      #####
######            annotations                                               #####
######            (e.g. .Values.nodeExporter.podSecurityPolicy.annotations) #####
#################################################################################


The Prometheus PushGateway can be accessed via port 9091 on the following DNS name from within your cluster:
prometheus-pushgateway.monitor.svc.cluster.local


Get the PushGateway URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace monitor -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace monitor port-forward $POD_NAME 9091

For more information on running Prometheus, visit:
https://prometheus.io/
```
**#( 12/21/20@ 9:16PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4**

   kubectl patch deployment prometheus-kube-state-metrics -n monitor --patch '{"spec": {"template": {"spec": {"nodeSelector": {"beta.kubernetes.io/arch": "amd64"}}}}}'
   
```
deployment.apps/prometheus-kube-state-metrics patched
```

**#( 12/21/20@ 9:41PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4**

   helm install grafana stablenew/grafana -n monitor
   
```  
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: This chart is deprecated
NAME: grafana
LAST DEPLOYED: Mon Dec 21 21:41:45 2020
NAMESPACE: monitor
STATUS: deployed
REVISION: 1
NOTES:
*******************
****DEPRECATED*****
*******************
* The chart is deprecated. Future development has been moved to https://github.com/grafana/helm2-grafana

1. Get your 'admin' user password by running:

   kubectl get secret --namespace monitor grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

2. The Grafana server can be accessed via port 80 on the following DNS name from within your cluster:

   grafana.monitor.svc.cluster.local

   Get the Grafana URL to visit by running these commands in the same shell:

     export POD_NAME=$(kubectl get pods --namespace monitor -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grafana" -o jsonpath="{.items[0].metadata.name}")
     kubectl --namespace monitor port-forward $POD_NAME 3000

3. Login with the password from step 1 and the username: admin
#################################################################################
######   WARNING: Persistence is disabled!!! You will lose your data when   #####
######            the Grafana pod is terminated.                            #####
#################################################################################
```

**#( 12/21/20@ 9:44PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy@master✔**

    kubectl get secret --namespace monitor grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
UEQGmcNP6GbEkOOMWKZOGNAnootvSTpzRzYHvTOE
```

**()#( 12/21/20@ 9:47PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy@master✗✗✗**

        export POD_NAME=$(kubectl get pods --namespace monitor -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grafana" -o jsonpath="{.items[0].metadata.name}")
     kubectl --namespace monitor port-forward $POD_NAME 3000

```
Forwarding from 127.0.0.1:3000 -> 3000
Forwarding from [::1]:3000 -> 3000
Handling connection for 3000
Handling connection for 3000
Handling connection for 3000
Handling connection for 3000
Handling connection for 3000
Handling connection for 3000
```
http://localhost:3000/login

**#( 12/21/20@10:39PM )( dbuddenbaum@dbuddenbaum-mbp ):~**

   helm install community prometheus-community/prometheus-blackbox-exporter -n monitor
   
```
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
NAME: community
LAST DEPLOYED: Mon Dec 21 22:39:35 2020
NAMESPACE: monitor
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
See https://github.com/prometheus/blackbox_exporter/ for how to configure Prometheus and the Blackbox Exporter.
```

![datasources/proemtheus](../kalaxy/images/set_prometheus_server_datasource.png)


## Thanos

[Monitoring Kubernetes workloads with Prometheus and Thanos](https://itnext.io/monitoring-kubernetes-workloads-with-prometheus-and-thanos-4ddb394b32c)