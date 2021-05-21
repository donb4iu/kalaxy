# Istio

[Quick Start: Unboxing Istio Service Mesh](https://kwonghung-yip.medium.com/quick-start-unboxing-istio-service-mesh-64b61eb319d7)

[Installing on the cluster](https://istio.io/latest/docs/setup/install/)

**#( 05/20/21@ 5:48PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/istio**

   curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.8.2  sh -
   
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
    100   102  100   102    0     0    214      0 --:--:-- --:--:-- --:--:--   213
    100  4573  100  4573    0     0   5954      0 --:--:-- --:--:-- --:--:--  5954
    
    Downloading istio-1.8.2 from https://github.com/istio/istio/releases/download/1.8.2/istio-1.8.2-osx.tar.gz ...
    Istio 1.8.2 Download Complete!
    
    Istio has been successfully downloaded into the istio-1.8.2 folder on your system.
    
    Next Steps:
    See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.
    
    To configure the istioctl client tool for your workstation,
    add the /Users/donbuddenbaum/Documents/rPi4/istio/istio-1.8.2/bin directory to your environment path variable with:
         export PATH="$PATH:/Users/donbuddenbaum/Documents/rPi4/istio/istio-1.8.2/bin"
    
    Begin the Istio pre-installation check by running:
         istioctl x precheck
    
    Need more information? Visit https://istio.io/latest/docs/setup/install/

**#( 05/20/21@ 5:51PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/istio**

   export PATH="$PATH:/Users/donbuddenbaum/Documents/rPi4/istio/istio-1.8.2/bin"

**#( 05/20/21@ 5:55PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/istio/istio-1.8.2**
   
   istioctl install -y
   
    Detected that your cluster does not support third party JWT authentication. Falling back to less secure first party JWT. See https://istio.io/v1.8/docs/ops/best-practices/security/#configure-third-party-service-account-tokens for details.
    ✔ Istio core installed
    ✔ Istiod installed
    ✔ Ingress gateways installed
    ✔ Installation complete
    
    
    
**#( 05/20/21@ 6:25PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml/knative@master✗✗✗**

   kubectl create -f https://github.com/knative/operator/releases/download/v0.23.0/operator.yaml
   
    customresourcedefinition.apiextensions.k8s.io/knativeeventings.operator.knative.dev created
    customresourcedefinition.apiextensions.k8s.io/knativeservings.operator.knative.dev created
    configmap/config-logging created
    configmap/config-observability created
    deployment.apps/knative-operator created
    clusterrole.rbac.authorization.k8s.io/knative-serving-operator-aggregated created
    clusterrole.rbac.authorization.k8s.io/knative-serving-operator created
    clusterrole.rbac.authorization.k8s.io/knative-eventing-operator-aggregated created
    clusterrole.rbac.authorization.k8s.io/knative-eventing-operator created
    clusterrolebinding.rbac.authorization.k8s.io/knative-serving-operator created
    clusterrolebinding.rbac.authorization.k8s.io/knative-serving-operator-aggregated created
    clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-operator created
    clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-operator-aggregated created
    serviceaccount/knative-operator created
    
**#( 05/20/21@ 6:26PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml/knative@master✗✗✗**

   kubectl get deployment knative-operator
   
    NAME               READY   UP-TO-DATE   AVAILABLE   AGE
    knative-operator   1/1     1            1           107s
    
**#( 05/20/21@ 6:34PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative@master✗✗✗**

   kubectl create -f serving.yaml
      
    namespace/knative-serving created
    knativeserving.operator.knative.dev/knative-serving created
   
**#( 05/20/21@ 6:34PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative@master✗✗✗**

   kubectl get deployment -n knative-serving
      
       NAME               READY   UP-TO-DATE   AVAILABLE   AGE
       activator          1/1     1            1           98s
       autoscaler         1/1     1            1           98s
       autoscaler-hpa     1/1     1            1           95s
       controller         1/1     1            1           97s
       istio-webhook      1/1     1            1           93s
       networking-istio   1/1     1            1           93s
       webhook            1/1     1            1           97s 
       
**#( 05/20/21@ 6:36PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative@master✗✗✗**

   kubectl get KnativeServing knative-serving -n knative-serving
   
    NAME              VERSION   READY   REASON
    knative-serving   0.23.0    True
**#( 05/20/21@ 6:41PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative@master✗✗✗**

   kubectl create -f eventing.yaml
   
    namespace/knative-eventing created
    knativeeventing.operator.knative.dev/knative-eventing created
**#( 05/20/21@ 6:44PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative@master✗✗✗**

   kubectl get deployment -n knative-eventing
   
    NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
    eventing-controller     1/1     1            1           2m50s
    eventing-webhook        1/1     1            1           2m49s
    imc-controller          1/1     1            1           2m44s
    imc-dispatcher          1/1     1            1           2m44s
    mt-broker-controller    1/1     1            1           2m41s
    mt-broker-filter        1/1     1            1           2m42s
    mt-broker-ingress       1/1     1            1           2m42s
    pingsource-mt-adapter   0/0     0            0           2m50s
    sugar-controller        1/1     1            1           2m41s
    
    
**#( 05/20/21@ 9:09PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative/helloworld@master✗✗✗**

   kubectl get svc $INGRESSGATEWAY --namespace istio-system
   
    NAME                    TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                                                                      AGE
    istio-ingressgateway    LoadBalancer   10.105.174.137   192.168.2.17   15021:31294/TCP,80:31844/TCP,443:30580/TCP,15012:31680/TCP,15443:31191/TCP   3h13m
    istiod                  ClusterIP      10.99.168.230    <none>         15010/TCP,15012/TCP,443/TCP,15014/TCP                                        3h14m
    knative-local-gateway   ClusterIP      10.110.187.116   <none>         80/TCP                                                                       154m
    
**#( 05/20/21@ 9:15PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative/helloworld@master✗✗✗**

   kubectl create -f helloworldsp-svc.yaml
   
    service.serving.knative.dev/helloworld-java created


**#( 05/21/21@ 2:43PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark@release-0.23✔**

   curl http://helloworld-java.default.example.com
   
    Hello SparkJava Sample v1%