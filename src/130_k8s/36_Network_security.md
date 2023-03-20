Rules:
Ingres -> direction to pod
Engress -> direction from pod

Connection:
pod for network policy:
```yaml
lables:
  role: db
```
network policy:
```yaml
apiVersion: networking.k8s.io./v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchiLabels:
      role: db
    policyTypes:
    - ingress  
    ingress:
    - from:      
      - podSelector:
       matchLabels:
         name: api-pod
       namespaceSelector: #restiction to allow only from one namespace
         matchLabels:
           name: prod
      - ipBlock:
         cidr: 192.168.5.10/32
      ports:
      - protocol: TCP
        port: 3306
    egress:
    - to:
      - ipBlock:
        cidr: 192.168.5.10/32
      port:
      - protocol: TCP
        port: 3306
```