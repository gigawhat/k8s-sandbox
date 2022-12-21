# K8s-sandbox

Welcome to the Kuberenetes Sandbox! This repository is meant for testing various features of the Kuberenetes container orchestration platform.


## Getting Started
To get started with this sandbox you'll need to have `kubectl`, `kind` and `task` installed.

Installation instructions for each can be found below:

* [`kubectl`](https://kubernetes.io/docs/tasks/tools/#kubectl)
* [`kind`](https://kind.sigs.k8s.io/docs/user/quick-start/)
* [`task`](https://taskfile.dev/installation/)

Once you have `kind` and `task` installed, you can clone this repository and create a local k8s cluster running some basic addons by running the default task.

```bash
task
task: [cluster] kind create cluster --name "k8s-sandbox" --image "kindest/node:v1.25.3@sha256:f52781bc0d7a19fb6c405c2af83abfeb311f130707a0e219175677e366cc45d1" --kubeconfig "k8s-sandbox.kubeconfig" --wait 5m
Creating cluster "k8s-sandbox" ...
 ✓ Ensuring node image (kindest/node:v1.25.3) 🖼
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
 ✓ Waiting ≤ 5m0s for control-plane = Ready ⏳ 
 • Ready after 19s 💚
Set kubectl context to "kind-k8s-sandbox"
You can now use your cluster with:

kubectl cluster-info --context kind-k8s-sandbox --kubeconfig k8s-sandbox.kubeconfig

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
task: [addons] kubectl --context "kind-k8s-sandbox" apply -k addons
serviceaccount/metrics-server created
clusterrole.rbac.authorization.k8s.io/system:aggregated-metrics-reader created
clusterrole.rbac.authorization.k8s.io/system:metrics-server created
rolebinding.rbac.authorization.k8s.io/metrics-server-auth-reader created
clusterrolebinding.rbac.authorization.k8s.io/metrics-server:system:auth-delegator created
clusterrolebinding.rbac.authorization.k8s.io/system:metrics-server created
service/metrics-server created
deployment.apps/metrics-server created
deployment.apps/shell created
apiservice.apiregistration.k8s.io/v1beta1.metrics.k8s.io created
```

This will create the local k8s cluster, deploy some basic addons to the cluster and create a kubeconfig file for the cluster named `k8s-sandbox.kubeconfig`. 

## Addons
* Kube-metrics - Needed for testing hpa
* Shell - Simple deployment that is used for exec'ing into a pod and running commands to test cluster features or addons

## Features
* HPA
    * [simple](hpa/simple/)
