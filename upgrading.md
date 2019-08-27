--- upgrading ---
- We can upgrade through various strategies
  - Upgrading all nodes at the same time
  - Upgrading the master and the each node one by one
  - Adding new nodes with upgraded components and decommissioning the old.

- Depending on your cluster setup, you can do:
  - cloud providers - already easy and taken care of in most cases
  - using kubeadm -  if you setup your cluster with it (kubeadm has to be upgraded first)
  - hard way - update all components individually.

 -- Nodes ---
 - After upgrading the kubelet on a node you should
 - updating the kubelet config and restart kubelet
   - `kubeadm upgrade node config --kubelet-version <kubelet version>`
   - `systemctl restart kubelet`
