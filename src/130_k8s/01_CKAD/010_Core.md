###CORE
* Create a namespace called 'mynamespace' and a pod with image nginx called nginx on this namespace
  * ```kubectl create ns mynamespace```
  * ```kubectl run nginx --image=nginx -n mynamespace```
* Create the pod that was just described using YAML
  * ```kubectl apply -f yaml```
* Create a busybox pod (using kubectl command) that runs the command "env". Run it and see the output
  * ```kubectl run busybox --image=busybox --command -- env```
  * ```kubectl run busybox --image=busybox -it --rm --command -- env```
* Get the YAML for a new namespace called 'myns' without creating it
  * ```kubectl create ns myns --dry-run=client -o yaml > ns.yaml```
* Get the YAML for a new ResourceQuota called 'myrq' with hard limits of 1 CPU, 1G memory and 2 pods without creating it
  * ```kubectl create quota myrq --hard=cpu=1,memory=1G,pods=2 --dry-run=client -o yaml```  
* Get pods on all namespaces
  * ```kubectl get po -A```
* Create a pod with image nginx called nginx and expose traffic on port 80
  * ```kubectl create po nginx --image-nginx --port=80```
* Change pod's image to nginx:1.7.1. 
  * ```kubectl set image pod/nginx nginx=nginx:1.7.1```
* Get nginx pod's ip created in previous step, use a temp busybox image to wget its '/'
  * `````# Get IP of the nginx pod```
  * ```NGINX_IP=$(kubectl get pod nginx -o jsonpath='{.status.podIP}')```
  * ```# create a temp busybox pod```
  * ```kubectl run busybox --image=busybox --env="NGINX_IP=$NGINX_IP" --rm -it --restart=Never -- sh -c 'wget -O- $NGINX_IP:80'```
* Get pod's YAML
  * ```kubectl get po podname -o yaml```
* Get information about the pod, including details about potential issues (e.g. pod hasn't started)
  * ```kubectl get po podname -o wide```
  * ```kubectl describe po podname```
* Get pod logs
  * ```kubectl logs po podname -c containerName```
* Execute a simple shell on the nginx pod
  * ```kubectl exec -it nginx -- /bin/sh```
* Create a busybox pod that echoes 'hello world' and then exits
  * ```kubectl run busybox -restart=Never --image=busybox -it -- echo "hello world"```
  * ```kubectl run busybox -restart=Never --image=busybox -it -- /bin/sh -c echo "hello world"```
* Do the same, but have the pod deleted automatically when it's completed
  * ```kubectl run busybox -restart=Never --image=busybox -it --rm -- echo "hello world"```
  * ```kubectl run busybox -restart=Never --image=busybox -it --rm -- /bin/sh -c echo "hello world"```
* Create an nginx pod and set an env value as 'var1=val1'. Check the env value existence within the pod
  * ```kubectl run nginx -restart=Never --image=nginx --env="var1=val1"```
  * ```kubectl exec nginx -it -- env```
  * ```kubectl exec nginx -it -- /bin/sh -c 'echo $var1' ```

Wrong
* Change pod's image to nginx:1.7.1. 
    * ```kubectl set image pod/nginx nginx=nginx:1.7.1```
* If pod crashed and restarted, get logs about the previous instance
  * ```kubectl logs nginx -p```

###MultiContainers
* Create a Pod with two containers, both with image busybox and command "echo hello; sleep 3600". Connect to the second container and run 'ls
  * ```kubectl ```
* Create a pod with an nginx container exposed on port 80. Add a busybox init container which downloads a page using "wget -O /work-dir/index.html http://neverssl.com/online". Make a volume of type emptyDir and mount it in both containers. For the nginx container, mount it on "/usr/share/nginx/html" and for the initcontainer, mount it on "/work-dir". When done, get the IP of the created pod and create a busybox pod and run "wget -O- IP"
  * ```kubectl run nginx --image=nginx --port=80```
  * init 
  ```yaml
    spec:
      initContainers:
      - args:
        - /bin/sh
        - -c 
        - wget -0 /work-dir/index.html http//neverssl.com/online
      image: busybox
      name: box
      volumeMounts:
      - name: vol
        mountPath: /work-dir
    ```
    * mount volume
    ```yaml
    containers:
      - image: nginx
      ...
      volumeMounts:
      - mountPath: /usr/share/nginx/html
        name: vol
      volumes: 
      - name: vol
        emptyDir: {}
    ```