### View cert using openssl
* ```openssl x509  -noout -text -in /etc/kubernetes/pki/apiserver.crt```

### View cert using kubeadm
* ```kubeadm certs check-expiration```

### Renew certs using kubeadm
* ```kubeadm certs renew``` - renew all cluster certs
* ```kubeadm certs renew apiserver``` - renew certs for apiserver only
