--- resource configurations ---
- you can back up all the resource configs by running
  - `kubectl get all --all-namespaces -o yaml > all-deploy-services.yaml`

--- etcd ---
- you can create set up the data directroy ie `--data-dir=<this path here>` defined in the etc config to be backed up preiodically
- you can use the etcd inbuild snapshot solution
  `ETCDCTL_API=3 etcdctl snapshot save <snapshot path>.db `
- you can view the status by using `ETCDCTL_API=3 etcdctl snapshot status <path to snapshot>.db`
> restoring backed up snapshot
- stop api-server
- restore the snapshot from the file created in the earlier commands
