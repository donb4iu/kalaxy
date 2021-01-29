[new relic infrastructure](https://one.newrelic.com/launcher/nr1-core.settings?pane=eyJuZXJkbGV0SWQiOiJrOHMtY2x1c3Rlci1leHBsb3Jlci1uZXJkbGV0Lms4cy1zZXR1cCIsImFjY291bnRJZCI6MzAzMzYwN30=&platform[timeRange][duration]=3600000&platform[$isFallbackTimeRange]=true&platform[accountId]=3033607)


   kubectl apply -f newrelic-ns.yaml

**#( 01/28/21@11:38PM )( donbuddenbaum@donbs-iMac ):~/Documents/rPi4/kalaxy/yaml/newrelic@master✗✗✗**
  
   kubectl apply -f newrelic-manifest.yaml -n newrelic
   
```   
serviceaccount/nri-bundle-nri-kube-events created
serviceaccount/nri-bundle-kube-state-metrics created
clusterrole.rbac.authorization.k8s.io/nri-bundle-nri-kube-events created
clusterrolebinding.rbac.authorization.k8s.io/nri-bundle-newrelic-infrastructure created
configmap/nri-bundle-nri-prometheus-config created
service/nri-bundle-kube-state-metrics created
daemonset.apps/nri-bundle-newrelic-logging created
clusterrole.rbac.authorization.k8s.io/nri-bundle-kube-state-metrics created
serviceaccount/nri-bundle-newrelic-infrastructure created
secret/nri-bundle-nri-kube-events-config created
mutatingwebhookconfiguration.admissionregistration.k8s.io/nri-bundle-nri-metadata-injection created
clusterrole.rbac.authorization.k8s.io/nri-bundle-newrelic-logging created
deployment.apps/nri-bundle-kube-state-metrics created
clusterrole.rbac.authorization.k8s.io/nri-bundle-nri-prometheus created
secret/nri-bundle-newrelic-infrastructure-config created
job.batch/nri-bundle-nri-metadata-injection-job created
deployment.apps/nri-bundle-nri-kube-events created
configmap/nri-bundle-newrelic-logging-fluent-bit-config created
clusterrolebinding.rbac.authorization.k8s.io/nri-bundle-nri-prometheus created
clusterrolebinding.rbac.authorization.k8s.io/nri-bundle-nri-metadata-injection created
secret/nri-bundle-newrelic-logging-config created
service/nri-bundle-nri-metadata-injection created
deployment.apps/nri-bundle-nri-metadata-injection created
clusterrolebinding.rbac.authorization.k8s.io/nri-bundle-nri-kube-events created
daemonset.apps/nri-bundle-newrelic-infrastructure created
secret/nri-bundle-nri-prometheus-config created
deployment.apps/nri-bundle-nri-prometheus created
serviceaccount/nri-bundle-nri-metadata-injection created
clusterrole.rbac.authorization.k8s.io/nri-bundle-nri-metadata-injection created
serviceaccount/nri-prometheus created
clusterrolebinding.rbac.authorization.k8s.io/nri-bundle-kube-state-metrics created
clusterrolebinding.rbac.authorization.k8s.io/nri-bundle-newrelic-logging created
serviceaccount/nri-bundle-newrelic-logging created
clusterrole.rbac.authorization.k8s.io/nri-bundle-newrelic-infrastructure created
```
##  New Relic Ubuntu   
[setup node](https://one.newrelic.com/launcher/nr1-core.settings?pane=eyJuZXJkbGV0SWQiOiJzZXR1cC1uZXJkbGV0LnNldHVwLW9zIiwiZGF0YVNvdXJjZSI6IlVCVU5UVSIsImFjY291bnRJZCI6MzAzMzYwN30=&platform[accountId]=3033607)

license key - 

### setup


```
### Add the New Relic Infrastructure Agent gpg key \

curl -s https://download.newrelic.com/infrastructure_agent/gpg/newrelic-infra.gpg | sudo apt-key add - && \

\

### Create a configuration file and add your license key \

echo "license_key: " | sudo tee -a /etc/newrelic-infra.yml && \

\

### Create the agent’s yum repository \

printf "deb [arch=amd64] https://download.newrelic.com/infrastructure_agent/linux/apt focal main" | sudo tee -a /etc/apt/sources.list.d/newrelic-infra.list && \

\

### Update your apt cache \

sudo apt-get update && \

\

### Run the installation script \

sudo apt-get install newrelic-infra -y
```


[explore](https://one.newrelic.com/launcher/nr1-core.explorer?pane=eyJuZXJkbGV0SWQiOiJucjEtY29yZS5saXN0aW5nIiwiZW50aXR5RG9tYWluIjoiSU5GUkEiLCJlbnRpdHlUeXBlIjoiSE9TVCIsImRvbWFpbiI6IkFQTSIsInR5cGUiOiJBUFBMSUNBVElPTiJ9&sidebars[0]=eyJuZXJkbGV0SWQiOiJucjEtY29yZS5jYXRlZ29yaWVzIiwicm9vdE5lcmRsZXRJZCI6Im5yMS1jb3JlLmxpc3RpbmciLCJkb21haW4iOiJBUE0iLCJ0eXBlIjoiQVBQTElDQVRJT04ifQ==&platform[accountId]=3033607)