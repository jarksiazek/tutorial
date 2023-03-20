* Multicontainters pod
  
  * Patterns
    * SIDECAR
      * e.g. log agent
    * ADAPTER
      * e.g. changing format logs 
    * AMBASSADOR
      * e.g. proxy logs to database   

* ```
  ...
  spec:
    - name: simple-webapp
      image: simple-webapp
      ports:
        - containerPort: 8080
    - name: log-agent
      image: log-agent
      ports:8081
        - 
  ```

* Container Logging
  
  * ```kubectl logs -f <pod-name>``` - option for one contrainer in the pod
  * ```kubectl logs -f <pod-name> <container-name>``` - option for multi contrainers in the pod  

* Monitoring Metrics Server
  
  * ```git clone http://github.com/kuberneter-incubator/metrics-server.git```
  * ```kubectl create -f deploy/1.8+/```
  * ```kubectl top node``` - getting some statictics from metrics server
  * ```kubectl top pods``` - getting some statictics from metrics server

###Pod Design

* Labels,Selectors and Annotations
  
  * ```
    apiVersion: v1
    kind: Pod
    metadata:
    name: simple-webapp
    labels:
     app:App1
     function:Front-end
    spec:
    contrainers:
    ...
    ```
  * ```kubectl get pod --selector app=App1```
  * ```
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
    name: simple-webapp
    labels:
     app:App1
     function:Front-end
    spec:
    replicas: 3
    selector:
     matchLabels:
      app: App1 # spec label -> template label
     template:
      metadata:
       labels:
        app: App1
        function: Front-end
       spec:
        containers:
        - name: simple-webapp
          image: simple-webapp
    ...
    ```

* Annotations
  
  * additional information

* Depolyment
  
  * CREATE - ```kubectl create -f deployment.yaml```
  * GET - ```kubectl get deployment```
  * UPDATE from file - ```kubectl apply -f deployment.yaml```
  * UPDATE from cmd - ```kubectl set image deployment nginx=nginx:1.9.1```
  * STATUS - ```kubectl rollout status deployment```
  * HISTORY - ```kubectl rollout history deployment```
  * ROLLBACK - ```kubectl rollout undo deployment```

* Deployment - update(rollaout) and rollback
  
  * Dyployment stategies
  * recreate - downtime (not default)
  * rolling update - default
  * ```kubectl rollout status deployment/myapp-deployment``` - status of rollout for deployment
  * ```kubectl rollout history deployment/myapp-deployment``` - history of rollout for deployment
  * ```kubectl rollout undo deployment/myapp-deployment``` - rollback

* Jobs
  
  * ```
    apiVersion: batch/v1
    kind: Job
    metadata:
     name: math-add-job
    spec:
     completions: 3 #create 3 jobs and 3 pods
     parallelism: 3 #optional, default is sequentional process 1 -> 2 -> 3
     template:
      spec:
       containers:
        - name: math-add
          image: ubuntu
          command: ['expr', '3', '+', '2']
      restartPolicy: Naver    
    ```
  * CREATE JOB - ```kubectl create -f job-definition.yaml```   
  * GET JOBS - ```kubectl get jobs```   
  * GET OUTPUT - ```kubectl logs <pod-name>```   
  * DELETE JOB - ```kubectl delete <job-name>```  

* CRON JOB
  
  * ```
    apiVersion: batch/v1beta1
    kind: CronJob
    metadata:
     name: reporting-cron-job
    spec:
     schedule: "*/1 * * * *"
     jobTemplate:
      spec:
       completions: 3 #create 3 jobs and 3 pods
       parallelism: 3 #optional, default is sequentional process 1 -> 2 -> 3
       template:
        spec:
         containers:
          - name: reporting-tool
            image: reporting-tool
         restartPolicy: Naver    
    ```
  * CREATE CRONJOB - ```kubectl create -f job-definition.yaml```   
  * GET CRONJOBS - ```kubectl get cronjobs```  

* SERVICES
  
  * Types
  
  * NodePort
    
    * external access to the app 
    
    * node (Node Port 30000-32767) -> Service (Port)-> PodPort (Target Port)
    
    * ```apiVersion:
        kind: Service
        metadata:
         name: app-service
        spec:
         type: NodePort
         ports:
      
          - targetPort: 80 #pod
            port: 80 #service
            nodePort: 3008 #node
      
         selector:
      
          app: myapp #data from POD metadata.labels
          type: front-end
      ```
    
    * Hitting app ```curl http://<service-ip>:<nodePort>```      
  
  * ClusterIP
    
    * connection between nodes and pods in the cluster (front->backend->db)
    * ```apiVersion:
      kind: Service
      metadata:
      name: back-end
      spec:
      type: ClousterIP
      ports:
      - targetPort: 80 #pod backend 
        port: 80 #service port
        selector:
        app: myapp #data from POD metadata.labels
        type: back-end
      ```
  
  * LoadBalancer

*INGRES

* ingress controller
  
  * nginx and many others 
  * use as a deployment
  * ```
    spec:
    contrainers:
    - name: nginx-ingress-controller
      image: quay.io/kubernetes-ingress-controller/nginix-ingress-controller:0.21.0
      args: 
    - /nginx-ingress-controller
    - --configmap=$(POD_NAMESPACE)/nginx-configuration
      env:
    - name: POD_NAME
      valueFrom:
       fieldRef:
        fieldPath:metadata.name
    - name: POD_NAMESPACE
      valueFrom:
       fieldRef:
        fieldPath: metadata.namespace
      ports:
    - name: http
      containerPort: 80
    - name: https
      containerPort: 443
  * service
    * ```
      apiVersion: v!
      kind: Service
      metadata:
      name: nginx-ingress
      spec:
      type: NodePort
      ports: 
    - port: 80
      targetPort: 80
      protocol: TCP
      name: http
    - port: 443
      targetPort: 443
      protocol: TCP
      name: https
      selector:
      name: nginx-ingress
  * serviceaccount   

* ingress resources

* ```apiVersion:
     kind: Ingress
     metadata:
      name: ingress-wear-watch
     spec:
      rules:
      - http:
         paths:
         - path: /wear
           pathType: Prefix
           backend:
            service:
             name: wear-service
             port:
              number: 80
         - path: /watch
           pathType: Prefix
           backend:
            service:
             name: watch-service
             port:
              number: 80     
  ```

* ```kubectl create ingress <ingress-name> --rule="host/path=service:port"```     

* ```kubectl create ingress ingress-test --rule="wear.my-online-store.com/wear*=wear-service:80"```     

* Network polices
  
  * ```apiVersion:
      kind: NetworkPolicy
      metadata:
       name: db-policy
      spec:
       podSelector:
    
        matchLabels:
         role: db
    
       policyTypes:
    
    - Ingress
    - Egress
      ingress:
    - from:
      - podSelector:
         matchLabels:
          name: api-pod
        namespaceSelector:
         matchLabels:
          name: prod
        ports:
      - protocol: TCP
        port: 3306
        engress:
      - to:
        - ipBlock:
          cidr: 192.168.6.10/32
          ports:
        - protocol: TCP
          port: 80
    ```
  
  * Volume - mounting space for storing data

* ```...
     spec:
  
      containers:
      - image: alpine
        name: alpine
        command: ["/bin/sh", "-c"]
        args: ["shuf -i 0-100 -n >>/opt/number.out;"]
        volumeMounts:
        - mountPath: /opt
          name: data-volume
  
     volume:
  
  - name: data-volume
    hostPath:
      path: /data
      type: Directory```
  ```

* example for using aws elasticBlockStore as volume
  
  * ```volumes:
    - name: data-volume
      awsElasticBlockStore:
       volumeID: <volumeId>
       fsType: ext4
    ```
  * Persistent volumes

* ```apiVersion:
     kind: PersistentVolume
     metadata: 
  
      name: pv-voll
  
     spec: 
  
      accessModes:
       - ReadWriteOnce
      capacity:
       storage: 1Gi
      awsElasticBlockStore:
       volumeID: <>volum-id>
       fsType: ext4
  
  * Persistent volume claims - connecting persistent volume with nodes
  ```

* ```apiVersion:
     kind: PersistentVolumeClaim
     metadata: 
  
      name: myclaim
  
     spec: 
  
      accessModes:
       - ReadWriteOnce
      resources:
       requests:
        storage: 500Mi```
  ```

* adding pv claim to pod/deployment/replicaset
  
  * ```apiVersion:
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
       claimName: myclaim```
    ```
