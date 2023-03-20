* Taint -> marks nodes
  
  * taint effects 
    
    * NoSchedule 
    
    * PreferNoSchedule - try to no schedule
    
    * NoExecute - pod will be evicted, no schedule

```bash
k taint nodes <node-name> key=value:taint-effect     
k taint nodes node1 app=blue:NoSchedule  
k taint nodes node1 app=blue:NoSchedule- #untaint
```

* Tolerant -> marks pods 

```yaml
...
spec:
    tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
```

* Affinity

```yaml
...
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: In
            values:
            - Large              
```
