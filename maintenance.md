--- cluster maintenance ---
-  To mark a node as unschedulable; meaning no pods will be Scheduled to it; you use:
  `kubectl cordon <node-name> --ignore daemon-sets`
  * --ignore-damonsets will ignore pods managed by a daemon-set
- To mark a node as unschedulable and evict pods that are not part of a replica-set, job etc
  you would use:
    `kubectl drain <node name > --force --ignore-daemonsets`
    * in cases where all are managed you would lose the --force flag
