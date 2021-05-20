[How to assign a namespace to certain node architectures](https://stackoverflow.com/questions/52487333/how-to-assign-a-namespace-to-certain-nodes)

# Namespaces by node architecture

## Enable-admission-plugins=PodNodeSelector

**dbuddenbaum@amd64-02:/etc/kubernetes/manifests$**
 
 sudo vi kube-apiserver.yaml


    apiVersion: v1
    kind: Pod
    metadata:
        annotations:
            kubeadm.kubernetes.io/kube-apiserver.advertise-address.endpoint: 192.168.2.56:6443
        creationTimestamp: null
        labels:
            component: kube-apiserver
            tier: control-plane
        name: kube-apiserver
        namespace: kube-system
    spec:
        containers:
        - command:
          - kube-apiserver
          - --advertise-address=192.168.2.56
          - --allow-privileged=true
          - --authorization-mode=Node,RBAC
          - --client-ca-file=/etc/kubernetes/pki/ca.crt
          - --enable-admission-plugins=NodeRestriction,PodNodeSelector

## Create Namespace

### amd64default 
```
apiVersion: v1
kind: Namespace
metadata:
  name: amd64default
  annotations:
      scheduler.alpha.kubernetes.io/node-selector: kubernetes.io/arch=amd64
spec: {}
status: {}
```

### arm64default 
```
apiVersion: v1
kind: Namespace
metadata:
  name: arm64default
  annotations:
      scheduler.alpha.kubernetes.io/node-selector: kubernetes.io/arch=arm64
spec: {}
status: {}
```