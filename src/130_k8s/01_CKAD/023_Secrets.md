###Secrets
* Create a secret called mysecret with the values password=mypass
  * ```kubectl create secret generic mysecret --from-literal=password=mypass```
* Create a secret called mysecret2 that gets key/value from a file 
  * ```kubectl create secret generic mysecret2 --from-file=username```
* Create a secret called mysecret2 that gets key/value from a file  
  * ```kubectl get secret mysecret3 -o jsonpath="{.data.username}" | base64 --decode```  
  * ```kubectl get secret mysecret2 -o json | jq -r .data.username | base64 -d  # on MAC it is -D```
* Create an nginx pod that mounts the secret mysecret2 in a volume on path /etc/foo
  * ```yaml
    containers:
    - name: demo 
      volumeMounts:
      - name: foo
        mountPath: "/etc/foo"
        readOnly: true
    volumes:
    - name: foo
      secret:
       secretName: mysecret2
       optional: false # default setting; "mysecret" must exist```
* Delete the pod you just created and mount the variable 'username' from secret mysecret2 onto a new nginx pod in env variable called 'USERNAME'
  * ```yaml
    spec:
      containers: 
      - name: demo
        env: 
        - name: USERNAME
          valueFrom:
            secretKeyRef:
              name: mysecret2
              key: username    
    ```