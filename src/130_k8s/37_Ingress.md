Ingress:
 cloud lb -> ingress controller -> ingress -> internal service -> pod

Ingress controller
- evaluates all the rules
- manages redirections
- entrypoint to cluster
- is installed in kube-system namespace

Ingress Yaml:
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
spec:
  rules:
    - host: myapp.com
      http:
        paths:
          - backend:
            serviceName: myapp-internal-service
            servicePort: 8080
```