###PersistentState
* Create busybox pod with two containers, each one will have the image busybox and will run the 'sleep 3600' command. Make both containers mount an emptyDir at '/etc/foo'. Connect to the second busybox, write the first column of '/etc/passwd' file to '/etc/foo/passwd'. Connect to the first busybox and write '/etc/foo/passwd' file to standard output. Delete pod.
* ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
  name: nginx
  spec:
    containers:
    - name: c1
      image: busybox
      command: ["sleep 3600"]
      volumeMounts:
      - mountPath: /etc/foo
        name: vol
    - name: c2
      image: busybox 
      command: ["sleep 3600"]
      volumeMounts:
      - mountPath: /etc/foo
        name: vol
    volumes:
    - name: vol
      emptyDir: {}
  ```
* Create a PersistentVolume of 10Gi, called 'myvolume'. Make it have accessMode of 'ReadWriteOnce' and 'ReadWriteMany', storageClassName 'normal', mounted on hostPath '/etc/foo'. Save it on pv.yaml, add it to the cluster. Show the PersistentVolumes that exist on the cluster
* ```yaml
  apiVersion: v1
  kind: PersistentVolume
  metadata:
  name: myvolume
  spec:
   capacity:
    storage: 10Gi
   accessModes:
    - ReadWriteOnce
    - ReadWriteMany
   persistentVolumeReclaimPolicy: Recycle
   storageClassName: normal
   hostPath:
     path: /etc/foo
   ```

* Create a PersistentVolumeClaim for this storage class, called 'mypvc', a request of 4Gi and an accessMode of ReadWriteOnce, with the storageClassName of normal, and save it on pvc.yaml. Create it on the cluster. Show the PersistentVolumeClaims of the cluster. Show the PersistentVolumes of the cluster
* ```yaml
  apiVersion: v1
  kind: PersistentVolumeClaim
  metadata:
    name: mypvc
  spec:
    storageClassName: normal
    accessModes:
     - ReadWriteOnce
    resources:
      requests:
        storage: 4Gi
  ```