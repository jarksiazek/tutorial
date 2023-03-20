* Create new config map
  
  ```bash
  kubectl create configmap webapp-config-map --from-literal=APP_COLOR=darkblue
  ```

* Pass data from configMap to pod envs (configMapRef)

```yaml
spec:
  containers:
  - envFrom:
    - configMapRef:
        name: webapp-config-map
    image: kodekloud/webapp-color
    name: webapp-color
```

* Pass data from configMap to pod envs (configMapKeyRef)

```yaml
spec:
  containers:
  - env:
    - name: APP_COLOR
      valueFrom:  
        configMapKeyRef:
          name: webapp-config-map #config map name
          key: APP_COLOR  
    image: kodekloud/webapp-color
    name: webapp-color
```
