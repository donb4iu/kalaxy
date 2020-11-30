#mysite - nginx

Directing Kubernetes traffic with Traefik [A step-by-step walkthrough on ingressing traffic into a Kubernetes-Raspberry Pi cluster.](https://opensource.com/article/20/3/kubernetes-traefik)

**[00:44:15]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy/yaml$** kubectl create configmap mysite-html --from-file index.html
```
configmap "mysite-html" created
```

**[23:35:41]donbuddenbaum@donbs-iMac:~/Documents/rPi4/kalaxy/yaml$** kubectl apply -f mysite.yaml --validate=false
```
deployment "mysite-nginx" configured
service "mysite-nginx-service" created
ingress "mysite-nginx-ingress" created
```

**#( 11/29/20@ 7:46PM )( dbuddenbaum@dbuddenbaum-mbp ):/private/etc**
   
   sudo vim hosts
   
   192.168.2.20 donb-k8s

[hello](http://donb-k8s/hello)
