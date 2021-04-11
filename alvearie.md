# Alvearie

## Install


kubectl create namespace alvearie

kubectl config set-context --current --namespace=alvearie

[helm install ingestion . -f loadbalancer-values.yaml](https://github.com/Alvearie/health-patterns/tree/main/clinical-ingestion/helm-charts/alvearie-ingestion#install-the-chart)


## FHIR Server Credentials

[https://github.com/Alvearie/health-patterns/tree/main/clinical-ingestion/helm-charts/alvearie-ingestion/charts/fhir](https://github.com/Alvearie/health-patterns/tree/main/clinical-ingestion/helm-charts/alvearie-ingestion/charts/fhir)

**#( 04/11/21@ 2:38AM )( dbuddenbaum@dbuddenbaum-mbp ):**~/Documents/rPi4/kalaxy@master✗✗✗

   kubectl exec ingestion-fhir-6f94b96865-xtk4s -n alvearie -c server -- cat server.xml | grep -A2 BasicRealm
```   
    <basicRegistry id="basic" realm="BasicRealm">
        <user name="fhiruser" password="integrati0n"/>
        <user name="fhiradmin" password="integrati0n"/>
```       
## FHIR [Operations](https://github.com/IBM/FHIR)


## FHIR UI - note requires proxy on 81

**#( 04/11/21@ 2:53AM )( dbuddenbaum@dbuddenbaum-mbp ):**~/Documents/rPi4/patient-browser/chart@master✔

   helm install fhir-ui . --set fhirServer=https://192.168.2.15/fhir-server/api/v4

```   
#( 04/11/21@ 3:16AM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/patient-browser/chart@master✔
   helm install fhir-ui1 . --set fhirServer=https://192.168.2.15/fhir-server/api/v4
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /Users/dbuddenbaum/.kube/config
NAME: fhir-ui1
LAST DEPLOYED: Sun Apr 11 03:18:52 2021
NAMESPACE: alvearie
STATUS: deployed
REVISION: 1
NOTES:
Welcome to the

       d8888 888                                    d8b
      d88888 888                                    Y8P
     d88P888 888
    d88P 888 888 888  888  .d88b.   8888b.  888d888 888  .d88b.
   d88P  888 888 888  888 d8P  Y8b     "88b 888P"   888 d8P  Y8b
  d88P   888 888 Y88  88P 88888888 .d888888 888     888 88888888
 d8888888888 888  Y8bd8P  Y8b.     888  888 888     888 Y8b.
d88P     888 888   Y88P    "Y8888  "Y888888 888     888  "Y8888

                               Clinical Data Ingestion Framework

Pattern: Sample FHIR User Interface

Get the application URL by running these commands:

  export POD_NAME=$(kubectl get pods --namespace alvearie -l "app.kubernetes.io/name=patient-browser,app.kubernetes.io/instance=fhir-ui1" -o jsonpath="{.items[0].metadata.name}")
  echo Patient Browser: http://127.0.0.1:/index.html
  kubectl --namespace alvearie port-forward $POD_NAME :
```        
    kubectl --namespace alvearie port-forward $POD_NAME 9091
```    
Forwarding from 127.0.0.1:9091 -> 9091
Forwarding from [::1]:9091 -> 9091  
```