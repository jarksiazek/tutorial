* Create new secret

```bash
kubectl create secret generic webapp-config-map --from-literal=APP_COLOR=darkblue
```

* Read secret 
```bash
kubectl get secret <SECRET_NAME> -o jsonpath="{.data.<DATA>}" | base64 --decode
```

- View secret values

- Pass data from secret to pod envs (secretRef) - passing whole file

```yaml
spec:
  containers:
  - envFrom:
    - secretRef:
        name: app-secret # k8s secret name   
    image: kodekloud/webapp-color
    name: webapp-color
```

* Pass data from secret to pod envs (secretKeyRef) - passing single value

```yaml
spec:
  containers:
  - env:
    - name: DB_PASSWORD
      valueFrom:
        secretKeyRef:
          name: app-secret # k8s secret name   
          key: DB_PASSWORD
    image: kodekloud/webapp-color
    name: webapp-color
```

* Pass data from secret to pod envs - passing whole file as volume (each value will be stored as separate file)

```yaml
valumes:
- name:
  secret:
    secretName: app-secret
```
