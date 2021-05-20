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
    
    
kubectl apply -f https://github.com/knative/operator/releases/download/v0.23.0/operator.yaml