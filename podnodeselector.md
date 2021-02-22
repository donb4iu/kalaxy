[How to assign a namespace to certain node architectures](https://stackoverflow.com/questions/52487333/how-to-assign-a-namespace-to-certain-nodes)

# Namespaces by node architecture

**First, you need to enable it in your kubernetes-apiserver:**

**Edit /etc/kubernetes/manifests/kube-apiserver.yaml:**

**--enable-admission-plugins=PodNodeSelector**


## amd64default 
```
kind: Namespace
apiVersion: v1
metadata:
  name: amd64default
  selfLink: /api/v1/namespaces/amd64default
  uid: 9aab3749-6195-45d1-bb0e-1a9e26fa24a1
  resourceVersion: '22212983'
  creationTimestamp: '2021-01-09T11:11:53Z'
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: >
      {"apiVersion":"v1","kind":"Namespace","metadata":{"annotations":{"scheduler.alpha.kubernetes.io/node-selector":"kubernetes.io/arch=amd64"},"name":"amd64default"},"spec":{},"status":{}}
    scheduler.alpha.kubernetes.io/node-selector: kubernetes.io/arch=amd64
spec:
  finalizers:
    - kubernetes
status:
  phase: Active
```

## arm64default 
```
kind: Namespace
apiVersion: v1
metadata:
  name: arm64default
  selfLink: /api/v1/namespaces/arm64default
  uid: 2c1332da-a132-47c6-8e5e-01ca5c671318
  resourceVersion: '22212981'
  creationTimestamp: '2021-01-09T11:11:53Z'
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: >
      {"apiVersion":"v1","kind":"Namespace","metadata":{"annotations":{"scheduler.alpha.kubernetes.io/node-selector":"kubernetes.io/arch=arm64"},"name":"arm64default"},"spec":{},"status":{}}
    scheduler.alpha.kubernetes.io/node-selector: kubernetes.io/arch=arm64
spec:
  finalizers:
    - kubernetes
status:
  phase: Active
```