---- Replication sets vs Replication controller ----
- replica controller does not require a `selector` property in the spec while a replica set does;

--- Deployments ---
- Similar to replica sets but allows for Rollbacks, rolling deploys etc

--- Namespaces --
- Used for separation and grouping of cluster resources

-- Services ---
- Allows for access to resources from outside world and within the cluster
> Types:
  - NodePort - Used to forward request to certain pods from a node port accessible to the outside world
  - Load balancers - used with supported cloud providers/plugins
  - Cluster ip - default type of service

---- Daemon sets ----
- used to ensure one copy of the item runs on all nodes
- kube scheduler has no effect on daemon sets
