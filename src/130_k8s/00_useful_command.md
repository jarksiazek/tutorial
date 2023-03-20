* bash cheets
  * ctrl-k, ctrl-u, ctrl-w, ctrl-y - cutting and pasting text in the command line
  * ctrl-a, go to beginning of the line 
  * ctrl-e, go to end of the line 
```yaml
TERMINAL Shortcuts Lists:  
Left            Move back one character
Right           Move forward one character
Ctrl+b          Move back one character
Ctrl+f          Move forward one character

Alt+Left        Move back one word
Alt+Right       Move forward one word
Alt+b           Move back one word
Alt+f           Move forward one word

Cmd+Left        Move cursor to start of line
Cmd+Right       Move cursor to end of line
Ctrl+a          Move cursor to start of line
Ctrl+e          Move cursor to end of line

Ctrl+d          Delete character after cursor
Backspace       Delete character before cursor

Alt+Backspace   Delete word before cursor
Ctrl+w          Delete word before cursor
Alt+w           Delete word before the cursor
Alt+d           Delete word after the cursor

Cmd+Backspace   Delete everything before the cursor
Ctrl+u          Delete everything before the cursor
Ctrl+k          Delete everything after the cursor

Ctrl+l          Clear the terminal

Ctrl+c          Cancel the command
Ctrl+y          Paste the last deleted command
Ctrl+_          Undo
```

* remove all services, pods, depoyments
  
  ```bash
  kubectl delete pods services deployments 
  ```

* curl - start image 
  
  ```bash
  kubectl run curl --image=radial/busyboxplus:curl -i --tty 
  ```

* connect to existing image 
  
  ```bash
  kubectl exec curl -it -- /bin/sh
  ```

* printenv
  
  ```bash
  kubectl exec <pod-name> -- printenv
  ```

* connect to postgres

```bash
kubectl run postgres --image=postgres -it --env="DB_HOST=docker.for.mac.host.internal" 
```

* create template for object

```bash
k create deploy <name> --dry-run=client -o yaml > s.yaml
```

* kubelet edit issue - replacing temp file 

```bash
k replace --force -f /tmp/kubectl-edit
```

* show yaml structure
```bash
kubectl explain pod  
kubectl explain pod --recursive
```

* get all serviceaccountnames from deployments
* ```kgd -A -ojsonpath={..spec.template.spec.serviceAccountName}```
* ```kgd  -A -o=jsonpath='{.items[*].spec.template.spec.serviceAccountName}'```

* secret 
  * get secret 
    * ```kubectl get secret <SECRET_NAME> -o jsonpath="{.data.<DATA>}" | base64 --decode```
    * ```kubectl get secret backend-secrets-sample-app -o jsonpath="{.data.CONNECTION_STRING}" | base64 --decode```

* postgress pod 
  * connection to db 
    * ```docker run -it --rm --name postgres -e POSTGRES_PASSWORD=jkdatabase postgres psql --host jkdatabase.cij5fwwuip0r.eu-west-2.rds.amazonaws.com -U jkdatabase -d postgres```
    * ```kubectl run postgresql-postgresql-client --rm --tty -i --restart='Never' --namespace default --image bitnami/postgresql --env="PGPASSWORD=<HERE_YOUR_PASSWORD>" --command -- psql --host <HERE_HOSTNAME=SVC_OR_IP> -U <HERE_USERNAME>```
  
* mysql pod
  * connect to db 
    * ```docker run -it --rm arm64v8/mysql mysql -hmy-sql-db-private.cij5fwwuip0r.eu-west-2.rds.amazonaws.com -udatabase1 -pdatabase1```
    * ```docker run -it --rm mysql mysql -hmy-sql-database1.cij5fwwuip0r.eu-west-2.rds.amazonaws.com -udatabase1 -p```
    * ```kubectl run mysql --rm --tty -i --restart='Never' --namespace default --image mysql --command -- mysql -hmy-sql-db-private.cij5fwwuip0r.eu-west-2.rds.amazonaws.com -udatabase1 -pdatabase1```

