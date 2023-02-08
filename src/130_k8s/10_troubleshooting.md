### Getting logs from node
* https://kubernetes.io/docs/tasks/debug/debug-cluster/
* connect to instance using ssm - ```aws ssm start-session i-0cfe219fca030a14a --region eu-west-2```
* get list on service on linux machine -- ```systemctl list-unit-files --type=service```
* get kublet logs - ```journalctl -fu kubelet.service ```
