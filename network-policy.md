--- network policies ---
- By default kubernetes has an "all allow" traffic policy;
- !! choose a network backend that supports network policies if this function is needed
  this means all pods can communicate with each other
- when you would need to restrict traffic between pods you would use the network policy object
- a network policy is linked to a pod
