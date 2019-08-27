> On Master
Kube api-server
etcd cluster
scheduler
controller manager
  - Node controller
  - Replication controller

> On Nodes
Container runtime engine (docker, containerd, rocket etc)
Kubelet
kube-proxy


--binaries for scratch setup
http://storage.googleapis.com/kubernetes-release/release/v1.14.4/bin/linux/amd64/

----- etcd ---
- distributed key value store(non tabular) - stored in pages or document
- stores
  - Nodes
  - Pods
  - Configs
  - Secrets
  - Accounts
  - Roles
  - Bindings
  - Others


----- scratch vs kubeadmn setup ----
- When setting up with kubeadmn most of the services ie api-server, etcd all run as pods on the master Node
- When setting up from scratch all this services run as systemd services on the master Node


---- kube controller manager ----
- a controller is a process that continuously monitors the state of various
  components within the system and tries to achieve desired state.

  - Node controller - monitors the status of the nodes through the kube api server
  - Replication controller - monitors status of replica sets
- Some other controllers include
  - deployment
  - cron
  - endpoint
  - PV protection
  - Job controller
  - Stateful set etc


------ kube scheduler ---
- Schedules pods on nodes depending on criteria
- Ranks node using a priority function to grade/rank nodes


------ kubelet ----
- Acts on kube scheduler's decision communicated through the api-server and
  deploys pods the monitors both pods and nodes and reports to api-server


----- kube-proxy ----
- Handles appropriate rules to forward traffic to particular services to correct back-end pods
-
