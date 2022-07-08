* Kube-apiserver
  * Authentication - Who can access the server?
    * Files - users and passwords
    * Files - users and token 
    * Certificates
    * External Authentication provider - LDAP
    * Service account
  * Authorization - What can they do ?
    * RBAC Authorization - role based access control
    * ABAC Authorization 
    * Node Authorization 
    * Webhook Mode
     

* Commands
  * ```kubectl create serviceaccount sa1```
  * ```kubectl get sa``` - list of service accounts 

* KubeConfig
  * ```kubectl config -h``` - view config help
  * ```kubectl config view``` - view default context
  * ```kubectl config view --kubeconfig=my-custom-config``` - view custom context
  * ```kubectl config use-context prod-user@production``` - change context to prod-user@production 

* Authorization
  * what can you do ```get```, ```delete```
  * Node - node requests
  * ABAC - Difficult to manage
  * RBAC - Recommended
    * define the groups
    * user -> role (eg. developer)
    * role is created using yaml
  * Webhook

* RBAC
  * role + role binding
  * ```kubectl get roles``` 
  * ```kubectl get rolebindings``` 
  * ```kubectl describe role developer``` 
  * ```kubectl describe rolebinding devuser-developer-binding``` 
  * ```kubectl auth can-i create depolyments``` 
  * ```kubectl auth can-i create depolyments --as dev-user``` 
  * ```kubectl auth can-i create depolyments --as dev-user --namespace test``` 
  * 