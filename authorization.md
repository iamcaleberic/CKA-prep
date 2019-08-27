---- Role based access control ---
- RBACs make use of api groups within the cluster to limit access and actions for specified resource(s)
- For most resources there are api verbs namely
  - list
  - get
  - create
  - update
  - delete
- create a role(s) and to match it to user(s) using a role bindings
- viewing the roles
  `kubectl get roles`
- viewing rolebindings
  `kubectl get rolebindings`
- view more info on a role use
  `kubectl describe role <role name>`
- view more info on rolebindings
  `kubectl describe rolebinding <role binding name> `
- to check if you have access(permission to perform) to a particular resource/action use
  `kubectl auth can-i <action>`
- if you are an admin you can impersonate a user
  `kubectl auth can-i <action name > --as dev-user`


----- Cluster Roles ---
- some resources or objects are scoped cluster wide that is where cluster roles come in
- can create cluster role for namespaces meaning access is granted across all namespaces
- to get api resources and groups use
  `kubectl api-resources`
  - find namespaced and non namspaced resources
    `kubectl api-resources --namespaced=<boolean>`
