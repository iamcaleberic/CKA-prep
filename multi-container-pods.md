----- multi container pods -----
- dont violate the "one process per container" principle
- Using several containers for an application is simpler to use, transparent and allows decoupling
- containers in a pod share the same IPC namespace and can also communicate with each other using process comms like
  SystemV or POSIX shared memory

> Use cases
  - sidecar containers - "help" main container
  - proxy(ies), bridges and adapters - connect main container to external world

> Accessing containers in multi-container pod

- `kubectl exec <pod name> -c <container> -- /bin/cat`

---- init Containers ---
- used to run a one a task before the app containers are started
- they always run to completion
- Each init container must complete successfully before the next one starts.
