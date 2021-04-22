# deploy traefik 

![traefik](images/traeficdashboard.png)

[k8s-code/ingress](https://github.com/initcron/k8s-code/tree/master/ingress)

## Manual 

[deploy](https://medium.com/kubernetes-tutorials/deploying-traefik-as-ingress-controller-for-your-kubernetes-cluster-b03a0672ae0c)

[metallb integration](https://www.devtech101.com/2019/02/23/using-metallb-and-traefik-load-balancing-for-your-bare-metal-kubernetes-cluster-part-1/
)
### Step 1: Enabling RBAC

kubectl create -f traefik-service-acc.yaml

``` 
serviceaccount "traefik-ingress" created
```

kubectl create -f traefik-cr.yaml

```
clusterrole.rbac.authorization.k8s.io “traefik-ingress” created
```

kubectl create -f traefik-crb.yaml

```
clusterrolebinding.rbac.authorization.k8s.io “traefik-ingress” created
```
### Step 2: Deploy Traefik to a Cluster

kubectl create -f traefik-deployment.yaml

```
deployment.extensions “traefik-ingress” created
```

kubectl --namespace=kube-system get pods

```
NAME                             READY     STATUS    RESTARTS   AGE....
traefik-ingress-xxxx             1/1       Running   0          1m
```

### Step 3: Create NodePorts for External Access

kubectl create -f traefik-svc.yaml

```
service “traefik-ingress-service” created
```

kubectl describe svc traefik-ingress-service --namespace=kube-system

```
Name:                     traefik-ingress-service
Namespace:                kube-system
Labels:                   <none>
Annotations:              <none>
Selector:                 k8s-app=traefik-ingress-lb
Type:                     NodePort
IP:                       10.102.215.64
Port:                     web  80/TCP
TargetPort:               80/TCP
NodePort:                 web  **30565**/TCP
Endpoints:                172.17.0.6:80
Port:                     admin  8080/TCP
TargetPort:               8080/TCP
NodePort:                 admin  **30729**/TCP
Endpoints:                172.17.0.6:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

### Step 4: Accessing Traefik using the “admin” NodePort **_30729_** (no configuration for frontend)

curl $(minikube ip):30565

```
404 page not found
```

### Step 5: Adding Ingress to the Cluster

kubectl create -f traefik-webui-svc.yaml

```
service “traefik-web-ui” created
```

kubectl describe svc traefik-web-ui --namespace=kube-system

```
Name:              traefik-web-ui
Namespace:         kube-system
Labels:            <none>
Annotations:       <none>
Selector:          k8s-app=traefik-ingress-lb
Type:              ClusterIP
IP:                10.98.230.58
Port:              web  80/TCP
TargetPort:        8080/TCP
Endpoints:         172.17.0.6:8080
Session Affinity:  None
Events:            <none>
```

kubectl create -f traefik-ingress.yaml

```
ingress.extensions “traefik-web-ui” created
```

echo "$(minikube ip) traefik-ui.minikube" | sudo tee -a /etc/hosts

```
192.168.99.100 traefik-ui.minikube
```

 http://traefik-ui.minikube:AdminNodePort

 
 ## traefik helm
 
 ### Reference
 
 - [Traefik Documentation - https://doc.traefik.io/traefik/v1.7/configuration/backends/kubernetes/](https://doc.traefik.io/traefik/v1.7/configuration/backends/kubernetes/)
 - [Deploying Traefik as Ingress Controller for Your Kubernetes Cluster](https://medium.com/kubernetes-tutorials/deploying-traefik-as-ingress-controller-for-your-kubernetes-cluster-b03a0672ae0c)
 - [How to Install Kubernetes Ingress (traefik) on a Raspberry Pi Cluster](https://medium.com/@geraldcroes/kubernetes-traefik-101-when-simplicity-matters-957eeede2cf8)
 - [Super Giant](https://supergiant.io/blog/using-traefik-as-ingress-controller-for-your-kubernetes-cluster/)
 
 ### Installation
 
 **#( 10/26/20@ 6:54PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy@master✗✗✗** kubectl create ns traefik
 ```
 namespace/traefik created
 ```
 **#( 10/26/20@ 6:55PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy@master✗✗✗** helm install my-traefik stable/traefik --set dashboard.enabled=true,serviceType=NodePort,dashboard.domain=dashboard.traefik,rbac.enabled=true,externalIP=192.168.2.56 --namespace traefik
 ```
   WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/donbuddenbaum/.kube/config
   WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/donbuddenbaum/.kube/config
   NAME: my-traefik
   LAST DEPLOYED: Mon Oct 26 18:57:07 2020
   NAMESPACE: traefik
   STATUS: deployed
   REVISION: 1
   TEST SUITE: None
   NOTES:
   1. Traefik has been started. You can find out the port numbers being used by traefik by running:
   
             $ kubectl describe svc my-traefik --namespace traefik
   
   2. Configure DNS records corresponding to Kubernetes ingress resources to point to the NODE_IP/NODE_HOST
 ```
 **[15:24:05]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy$** kubectl describe svc my-traefik --namespace traefik
 ```
 Name:                     my-traefik
 Namespace:                traefik
 Labels:                   app=traefik
                           app.kubernetes.io/managed-by=Helm
                           chart=traefik-1.87.2
                           heritage=Helm
                           release=my-traefik
 Annotations:              meta.helm.sh/release-name: my-traefik
                           meta.helm.sh/release-namespace: traefik
 Selector:                 app=traefik,release=my-traefik
 Type:                     NodePort
 IP:                       10.96.205.156
 External IPs:             192.168.2.56
 Port:                     https  443/TCP
 TargetPort:               httpn/TCP
 NodePort:                 https  30337/TCP
 Endpoints:                10.244.3.2:8880
 Port:                     http  80/TCP
 TargetPort:               http/TCP
 NodePort:                 http  31295/TCP
 Endpoints:                10.244.3.2:80
 Session Affinity:         None
 External Traffic Policy:  Cluster
 Events:                   <none>
 ```
 
 **[16:16:47]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy$** kubectl describe svc my-traefik-dashboard --namespace=traefik
 ```
 Name:              my-traefik-dashboard
 Namespace:         traefik
 Labels:            app=traefik
                    app.kubernetes.io/managed-by=Helm
                    chart=traefik-1.87.2
                    heritage=Helm
                    release=my-traefik
 Annotations:       meta.helm.sh/release-name: my-traefik
                    meta.helm.sh/release-namespace: traefik
 Selector:          app=traefik,release=my-traefik
 Type:              ClusterIP
 IP:                10.96.78.171
 Port:              dashboard-http  80/TCP
 TargetPort:        8080/TCP
 Endpoints:         10.244.3.2:8080
 Session Affinity:  None
 Events:            <none>
 ```
 
 
 **/etc/hosts** 192.168.2.50 dashboard.traefik
 
 
 ### uninstall
 helm uninstall mytraefik -n traefik
 
 ## examples
 
 **[16:28:27]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy/deployments$** kubectl create -f animals-deployments.yaml --validate=false
 ```
 deployment "bear" created
 deployment "moose" created
 deployment "hare" created
 ```
 **[16:33:41]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy/deployments$** kubectl create -f animals-svc.yaml --validate=false
 ```
 service "bear" created
 service "moose" created
 service "hare" created
 ```
 **[16:39:32]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy/deployments$** kubectl create -f animals-ingress.yaml --validate=false
 ```
 ingress "animals" created
 ```
 
 ### Urls for examples
 - [dashboard](http://dashboard.traefik:31295/dashboard/)
 - [moose](http://animals.traefik:31295/moose/)
 - [bear](http://animals.traefik:31295/bear/)
 - [hare](http://animals.traefik:31295/hare/)
  
  
## Traefik

deploy


**#( 04/12/21@10:12AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/2-Traefik@master✗✗✗**
  
   kubectl describe svc traefik-ingress-service --namespace=kube-system
   
```   
Name:                     traefik-ingress-service
Namespace:                kube-system
Labels:                   app=traefik
Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                            {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"app":"traefik"},"name":"traefik-ingress-service","namespace":"...
Selector:                 k8s-app=traefik-ingress-lb
Type:                     LoadBalancer
IP:                       10.106.124.204
IP:                       192.168.2.20
LoadBalancer Ingress:     192.168.2.20
Port:                     web  80/TCP
TargetPort:               80/TCP
NodePort:                 web  32538/TCP
Endpoints:                10.244.4.14:80,10.244.9.25:80
Port:                     https  443/TCP
TargetPort:               443/TCP
NodePort:                 https  31837/TCP
Endpoints:                10.244.4.14:443,10.244.9.25:443
Port:                     metrics  8080/TCP
TargetPort:               8080/TCP
NodePort:                 metrics  30359/TCP
Endpoints:                10.244.4.14:8080,10.244.9.25:8080
Session Affinity:         None
External Traffic Policy:  Local
HealthCheck NodePort:     32649
Events:
  Type    Reason        Age                     From             Message
  ----    ------        ----                    ----             -------
  Normal  nodeAssigned  2m38s (x659 over 3d9h)  metallb-speaker  announcing from node "amd64-05"
```

**#( 04/13/21@12:29PM )( dbuddenbaum@dbuddenbaum-mbp ):/private/etc**

   sudo vi hosts
   
```   
192.168.2.50 animals
192.168.2.50 donb-k8s
```


[bear](http://animals:32538/bear/)

[moose](http://animals:32538/moose/)

[hare](http://animals:32538/hare/)

[dashboard](http://192.168.2.20:8080/dashboard/)

[dashboard](http://animals:30359/dashboard/)

[donbs cloud](http://donb-k8s:32538/hello/)

[visualizer](http://donb-k8s:32538/visualizer/)