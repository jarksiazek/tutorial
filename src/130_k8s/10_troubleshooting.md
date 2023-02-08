### Getting logs from node
* https://kubernetes.io/docs/tasks/debug/debug-cluster/
* connect to instance using ssm - ```aws ssm start-session i-0cfe219fca030a14a --region eu-west-2```
* get list on service on linux machine -- ```systemctl list-unit-files --type=service```
* get kublet logs - ```journalctl -fu kubelet.service ```


### Testing role in the pod
* create a fake service account and bind to selected role 
```{toggle}
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
