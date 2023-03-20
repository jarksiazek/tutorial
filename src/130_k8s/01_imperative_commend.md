#### [Kubectl Reference Docs](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)

#### Deployment

```bash
kubectl create deploy <deply-name> --image <image-name> --replicas=4
```

```bash
kubectl create deploy <deply-name> --image <image-name> --dry-run=client -o yaml > deploy.yaml
```

```bash
kubectl scale deploy <deply-name> --replicas=4
```

#### Service

```bash
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
```

```bash
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml
```

```bash
kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml
```
