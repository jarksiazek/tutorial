### to be repeated
* secrets
* cluster maintenance
  * backup and restore
* crp
* storage

* Test 3
  * 2, 5, 7 ,9



### Killet sh 
* 25 - backup and restore 
  * ```ETCDCTL_API=3 etcdctl -endpoints=https://127.0.0.1:2379  --cacert=<trusted-ca-file> --cert=<cert-file> --key=<key-file> snapshot save <backup-file-location> ``` - backup commend  
  * ```ETCDCTL_API=3 etcdctl snapshot restore --data-dir <data-dir-location> snapshot-location-name ``` - restore snapshot
  * modify ```-dir-name``` on /var/kubernetes/manifests/etcd.yaml  
