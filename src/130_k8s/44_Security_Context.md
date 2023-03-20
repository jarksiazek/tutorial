* Kubernetes security
  
  * pod context security
  
  ```yaml
  apiVersion: v1
  kind: Pod
  ..
  spec:
      securityContext:
          runAsUser: 1000
  ...
  ```
  
  * container context security
  
  ```yaml
  spec:
      containsers:
        - name: ubuntu
          image: ubuntu
          command: ["sleep","3600"]    
          securityContext:
              runAsUser: 1000
              capabilities: 
                  add: ["MAC_ADMIN"]
  ```
