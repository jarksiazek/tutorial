###ServiceAndNetworking
* Create a pod with image nginx called nginx and expose its port 80
  * ```kubectl run nginx --image=nginx --restart=Never --port=80 --expose```
* Confirm that ClusterIP has been created. Also check endpoints
  * ```kubectl get svc```
  * ```kubectl describe svc nginx```
* Get service's ClusterIP, create a temp busybox pod and 'hit' that IP with wget
  * ```kubectl get svc nginx -o wide```
  * ```kubectl run --rm -it tempod --image=busybox -- wget 12.121.121.12:80```
* Convert the ClusterIP to NodePort for the same service and find the NodePort port. Hit service using Node's IP. Delete the service and the pod at the end.
  * ```yaml
    spec:
     type: NodePort
     selector:
       app.kubernetes.io/name: MyApp
     ports:
     - port: 80
       targetPort: 80
    ```
  * ```kubectl get svc```  -> node - port
  * ```kubectl get po nginx -o wide``` -> node ip
  * ```kubectl run --rm -it tempod --image=busybox -- wget -O- nodeId:nodePort```
* Create a deployment called foo using image 'dgkanatsios/simpleapp' (a simple server that returns hostname) and 3 replicas. Label it as 'app=foo'. Declare that containers in this pod will accept traffic on port 8080 (do NOT create a service yet)
  * ```kubectl create deploy foo --image=dgkanatsios/simpleapp --replicas=3 --label=app=foo --port=8080 --dry-run=client -o yaml > dep.yaml``` 
* Get the pod IPs. Create a temp busybox pod and try hitting them on port 8080
  * ```kubectl get po ```
  * ```kubectl run --rm -it tempod --image=busybox -- wget -O- podId:8080```
* Create a service that exposes the deployment on port 6262. Verify its existence, check the endpoints
  * ```kubectl create service clusterip my-cs --tcp=6262:8080```
  * ```yaml
    spec:
     selector:
      app: foo
     ports:
       - protocol: TCP
         port: 6262
         targetPort: 8080
    ```
* Create a temp busybox pod and connect via wget to foo service. Verify that each time there's a different hostname returned. Delete deployment and services to cleanup the cluster
  * ```kubectl temp --image=busybox --rm -it -- wget -O- <service_name>:6262```

* Create an nginx deployment of 2 replicas, expose it via a ClusterIP service on port 80. Create a NetworkPolicy so that only pods with labels 'access: granted' can access the deployment and apply it
  * ```kubectl create deploy nginx --image=nginx --port=80 --replicas=2```
  * ```kubectl expose deploy nginx --port=80 --targetPort=80```
  * ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
    name: nginx-network-policy
    namespace: default
    spec:
      podSelector:
        matchLabels:
          name: nginx
        policyTypes:
        - ingress
        ingress:
        - from:
          - podSelector:
            matchLabels:
              access: granted   
    ```