* Job - set of task to be completed
  * ```docker run ubuntu expr 3 + 2``` - docker example
  * ```yaml
    ...
    spec:
      containers:
      - image: ubuntu
        name: math-add      
        command: ['expr', '3', '+', '2']
      restartPolicy: never
  * ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: math
    spec:
      completions: 3 # number of completion - default is 1
      parallelism: 3 # execute 3 pods/tasks in the same time
      template:
        spec:
          containers:
          - name: math
            image: ubuntu
            command: ['expr', '3', '+', '2']
            restartPolicy: Never 
            backoffLimit: 4    

* CronJobs - scheduled jobs
  * ```yaml
    apiVersion: batch/v1
    kind: CronJob
    metadata:
      name: cron-example
    spec:
      schedule: "* * * * *"
      jobTemplate:
        spec:
          completions: 3 # number of completion - default is 1
          parallelism: 3 # execute 3 pods/tasks in the same time
          template:
            spec:
              containers:
              - name: math
                image: ubuntu
                command: ['expr', '3', '+', '2']
              restartPolicy: Never 
              backoffLimit: 4