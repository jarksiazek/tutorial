### Node not ready
* ```ssh worker-node``` - connect to worker node by ssh
* ```service kublet status``` - get service status
* ```systemclt daemon-reload``` - Reload the systemd manager configuration
* ```systemclt restart kublet``` - restart kublet service
* examples 
  * https://www.youtube.com/watch?v=0FoASYTK7tA

### Update cluster 
* ```ssh worker-node``` - get into the worker node
* ```kubeadm --version``` - check the version of the node
* ```kubelet --version``` - check the kubelet version 
* use this for upgrding worker and master nodes : https://v1-25.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

### JOIN WORKER TO CLUSTER
* ```kubeadm token create --print-join-command``` - control master node generate command and then use is on the worker node 

### Getting logs from node
* https://kubernetes.io/docs/tasks/debug/debug-cluster/
* connect to instance using ssm - ```aws ssm start-session i-0cfe219fca030a14a --region eu-west-2```
* get list on service on linux machine -- ```systemctl list-unit-files --type=service```
* get kublet logs - ```journalctl -fu kubelet.service ```
* kublet config file - node - ```/etc/kubernetes/kubelet.conf```
* kublet config file - node - ```/var/lib/kubelet/config.yaml```


### Testing role in the pod
* create a fake service account and bind to selected role
  <details>
    <summary>Click me</summary>
      
    ```bash
    cat <<EOF | kubectl apply -f -
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: kyverno-policy-test
      namespace: fake-kyverno-ns
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      labels:
        app.kubernetes.io/component: runtime-test
        app.kubernetes.io/managed-by: pm119
        app.kubernetes.io/name: cd-systems
        app.kubernetes.io/part-of: cd-systems
        runtime.babylontech.co.uk/cd-system: runtime-test
        squad: runtime
        tribe: cloud
      name: cd-systems:creator-kyverno-test
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: cd-systems:creator
    subjects:
    - kind: ServiceAccount
      name: kyverno-policy-test
      namespace: fake-kyverno-ns
    EOF
    ```
  </details>
* run a pod with created service account
  <details>
    <summary>Click me</summary>

    ```bash
    cat <<EOF | kubectl apply -f -
      apiVersion: v1
      kind: Pod
      metadata:
        name: shell-demo
        namespace: fake-kyverno-ns
      spec:
        volumes:
        - name: shared-data
          emptyDir: {}
        containers:
        - name: nginx
          image: nginx
          volumeMounts:
          - name: shared-data
            mountPath: /usr/share/nginx/html
        hostNetwork: true
        dnsPolicy: Default
        serviceAccountName: kyverno-policy-test
      EOF
     ```
    </details>
 * go to the pod 
    <details>
      <summary>Click me</summary>

      ```bash
      k exec -it nginx -n fake-kyverno-ns -- /bin/sh
       ```
      </details>
  * accessing the Kubernetes API from a Pod - https://kubernetes.io/docs/tasks/run-application/access-api-from-pod/
    <details>
      <summary>Click me</summary>

      ```bash
      # Point to the internal API server hostname
      APISERVER=https://kubernetes.default.svc

      # Path to ServiceAccount token
      SERVICEACCOUNT=/var/run/secrets/kubernetes.io/serviceaccount

      # Read this Pod's namespace
      NAMESPACE=$(cat ${SERVICEACCOUNT}/namespace)

      # Read the ServiceAccount bearer token
      TOKEN=$(cat ${SERVICEACCOUNT}/token)

      # Reference the internal certificate authority (CA)
      CACERT=${SERVICEACCOUNT}/ca.crt

      # Explore the API with TOKEN
      curl --cacert ${CACERT} --header "Authorization: Bearer ${TOKEN}" -X GET ${APISERVER}/api
       ```
      </details>     
 * curl post for creating new namespace using testing role
    <details>
      <summary>Click me</summary>

      ```bash
      curl --cacert ${CACERT} --header "Authorization: Bearer ${TOKEN}" -X POST ${APISERVER}/api/v1/namespaces/ \
      -H 'Content-Type: application/json' \
      -d '
      {"apiVersion": "v1","kind": "Namespace","metadata":  
      {"name": "mynewnamespace", "labels": {"app.kubernetes.io/name":"mynewnamespace", "squad":"runtime", "tribe":"cloud"}}}'
       ```
      </details>
