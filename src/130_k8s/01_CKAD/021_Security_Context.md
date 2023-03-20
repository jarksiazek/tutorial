###SecurityContext
* Create the YAML for an nginx pod that runs with the user ID 101. No need to create the pod
  * ```
    spec:
      securityContext:
        runAsUser: 101  
      containers:
      - name: demo```
* Create the YAML for an nginx pod that has the capabilities "NET_ADMIN", "SYS_TIME" added to its single container
  * ```
    spec:
      containers:
      - name: demo
      securityContext:
        capabilities:
          add: ["NET_ADMIN", "SYS_TIME"]
    ```