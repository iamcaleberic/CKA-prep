--- config maps---
- Used to provide env variables for resources in a kubernetes Cluster
- They follow a key value store method
- can be created imperatively by
  `kubectl create configmaps --from-relative=key=value`


--- Secrets ---
- used to store sensitive values in a cluster, unlike config maps where they are in plain text
- can be created in imperatively by
  `kubectl create secret generic <secret name> --from-literal=key=value`
