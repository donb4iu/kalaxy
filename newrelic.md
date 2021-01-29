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