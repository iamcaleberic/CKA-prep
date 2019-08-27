##### Notes
- Static pods
- Ingress and Ingress rules
- Stateful sets
- Daemons sets
- Networking other than cloud provider plugins
- Using containerd directly
- Jobs running on intervals and with certain conditions
- Setting up TLS certificates on cluster
- Auto scaling groups
- Volume claims in files
- Networking policies withing pods
- Rollbacks
- Using a scratch disk/ setting up one
- Filter out pods
- Setting up etcd
- Using weaveworks
- Put memory limits on a namespace
- Getting skeleton yaml
  `kubectl create deployment nginx --image=nginx --dry-run -o yaml`
-  Exposing a pod to Nodeport
  `kubectl expose pod <pod_name> --type=NodePort --port=80`
- Edit a pod
  `kubectl edit pod <pod_name>`
- Scaling up or down
  `kubectl scale <something> --replicas=<arbitrary no>``
- If api-server is down and you cant access components using kubectl; you can always go down a level lower and use docker alternatives
  - For logs example
    - `docker ps`
    - `docker logs <container name>`
- get pods using the certificate with kubectl
  - kubectl get pods --server <server-name>:<port> --client-key <user key> --client-certificate <user cert > --certificate-authority <ca cert>

- setup nginx deployment
#### reminder
- understand what the question is asking a pod is not a deployment
- understand difference between creating using imperative commands and using definition files
> https://kubernetes.io/docs/tasks/
