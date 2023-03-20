* Volume
  * added to pod 
  * node dictionary
  ```yaml
  ...
  spec:
    containers:
      - image: alpine
        ...
        volumeMounts:
        - mountPath: /opt
          name: data-volume  
    volumes:
      - name: data-volume #data created on the node, good for single node  
        hostPath:
          path: /data
          type: Directory
  ```
  * elastic block store
  ```yaml
  spec:
    volumes:
    - name: data-view
      awsElasticBlockStore:
      volume: <volume-id>
      fsType: ext4 # file system type  
  ```
  
* Persistent Volume 
  * separate object for storing volume
  * one object for many pods
  ```yaml
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: pv-vol1
  spec:
    accessModes:
    - ReadWriteOnce
    capacity:
      storage: 1Gi 
    awsElasticBlockStore:
      volumeId: <volume-id>
      fsType: ext4 
  ```
  
* Persistent Volume Claim 
  * making pv available for pod 
  * one 1 PV for 1 PVC, PV must be bigger than PVC 
  * PVC, PC matching criteria -> sufficient capacity, access mode, volume modes, storage class, selector
  ```yaml
  apiVersion: v1
  kind: PersistentVolumeClaim
  metadata:
    name: myclaim
  spec:
    accessModes:
    - ReadWriteOnce:
    resources:
      requests:
        storage: 500Mi
  ```
  
* adding PVC to pod
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
  name: mypod
  spec:
  containers:
  - name: myfrontend
    image: nginx
    volumeMounts:
    - mountPath: "/var/www/html"
      name: mypd
      volumes:
  - name: mypd
    persistentVolumeClaim:
    claimName: myclaim
  ```