###ConfigMaps
* Create a configmap named config with values foo=lala,foo2=lolo
  * ```kubectl create configmap config --from-literal=foo=lala --from-literal=foo2=lolo```
* Display its values
  * ```kubectl get cm config -o yaml```
* Create and display a configmap from a file
  * ```kubectl create configmap config --from-file=config.txt```
* Create and display a configmap from a .env file
  * ```kubectl create configmap3 config --from-env-file=config.env```
  * ```kubectl get cm configmap3 -o yaml```
* Create and display a configmap from a file, giving the key 'special'
  * ```kubectl create configmap4 config --from-file=special=config.env```
* Create a configMap called 'options' with the value var5=val5. Create a new nginx pod that loads the value from variable 'var5' in an env variable called 'option'
  * ```kubectl create configmap options --from-literal=var5=val5```
  * ```kubectl run nginx --image=nginx```
  * ```
    env:
      - name: option 
        valueFrom: 
          configMapKeyRef:
            name: options
            key: val5
    ```
* Create a configMap 'anotherone' with values 'var6=val6', 'var7=val7'. Load this configMap as env variables into a new nginx pod    
  * ```kubectl create configmap anotherone --from-literal=var6=val6  --from-literal=var7=val7```
  * ```kubectl run nginx --image=nginx```
  * ```
    envFrom:
    - configMapRef: # different from the previous one, was 'configMapKeyRef'
      name: anotherone
          
    ```
* Create a configMap 'cmvolume' with values 'var8=val8', 'var9=val9'. Load this as a volume inside an nginx pod on path '/etc/lala'. Create the pod and 'ls' into the '/etc/lala' directory.
  * ```kubectl create configmap cmvolume --from-literal=var8=val8 --from-literal=var9=val9```
  * ```kubectl run nginx --image=nginx```
  * ```yaml
    spec:
      containers:
        - name: demo
          volumeMounts:
          - name: config
            mountPath: /etc/lala
            readOnly: true
      volumes:
        - name: config 
          configMap:
            name: cmvolume
    ```
  * kubectl exec -it nginx -- /bin/sh -c "ls /etc/lala"


### To do - Different type of mounting cm in the pod
