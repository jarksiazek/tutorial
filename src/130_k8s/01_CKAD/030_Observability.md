###Observability
* Create an nginx pod with a liveness probe that just runs the command 'ls'. Save its YAML in pod.yaml. Run it, check its probe status, delete it.
  * ```kubectl run nginx -image=nginx --dry-run=client -o yaml > pod.yaml```
  * ```
    spec:
      containers:
      - name: demo
        livenessProbe:
          exec:
            command:
            - ls
    ```
    * ```kubectl apply -f pod.yaml```
    * ```kubectl describe po nginx```
    * ```kubectl delete po nginx```
* Create an nginx pod (that includes port 80) with an HTTP readinessProbe on path '/' on port 80. Again, run it, check the readinessProbe, delete it.
  * ````kubectl run nginx --image=nginx  --dry-run=client --port=80 -o yaml > pod.yaml````
  * ```yaml
    spec:
      containers:
      - name: nginx
        readinessProbe:
          path: /
          port: 80
    ```
  * ```kubectl apply -f pod.yaml```
  * ```kubectl describe po nginx```
  * ```kubectl delete po nginx```

* Lots of pods are running in qa,alan,test,production namespaces. All of these pods are configured with liveness probe. Please list all pods whose liveness probe are failed in the format of <namespace>/<pod name> per line.
  * ```kubectl get events -A | grep -i "Liveness probe failed" | awk '{print $1,$5}'```

* Create a busybox pod that runs 'i=0; while true; do echo "$i: ((i+1))"; sleep 1; done'. Check its logs
  * ```kubectl run busybox -image=busybox -- /bin/sh -c  'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done''```
  * ```kubectl logs busybox```

* Create a busybox pod that runs 'ls /notexist'. Determine if there's an error (of course there is), see it. In the end, delete the pod
  * ```kubectl run busybox --image=busybox -- ls/notexist ```
  * ```kubectl describe pod busybox```
  * ```kubectl logs busybox```

* Get CPU/memory utilization for nodes (metrics-server must be running)
  * ```kubectl top nodes```