###ServiceAccount
* See all the service accounts of the cluster in all namespaces
  * ```kubectl get sa -A```
* Create a new serviceaccount called 'myuser'
  * ```kubectl create sa myuser```
* Create an nginx pod that uses 'myuser' as a service account
  * ```yaml
    spec:
      serviceAccountName: build-robot 
    ```