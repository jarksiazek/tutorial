### Elastic Deployment Options for Updates ###
![](images/aim10.jpg)

* All at once     
    * faster deployment 
    * application has downtime
    * great for quick iterations in development environment
    * no additional cost  
    ![](images/aim3.jpg)
    
* Rolling 
    * application is running below capacity
    * can set bucket size
    * application is running both versions simultaneously
    * no additional cost 
    * long deployment   
    ![](images/aim4.jpg)

* Rolling with additional batches 
    * application is running at capacity
    * can set the bucket size
    * small additional cost
    * additional batch is removed at the end of the deployment
    * long deployment
    * good for prod
    ![](images/aim5.jpg)

* Immutable
    * zero downtime
    * new code is deployed to new instances on temporary ASG
    * high cost, double capacity
    * longest deployment
    * quick rollback in case of failures (just terminate new ASG)
    * great for prod  
    ![](images/aim6.jpg)

* Blue/Green
    * Not a "direct failure" of Elastic Beanstalk
    * Zero downtime and release facility
    * create a new "stage" environment and deploy v2 there 
    * the new environment (green) can be validated independently and roll back if issues
    * Route 53 can be set up using weighted policies to redirect a little bit of traffic to stage environment
    * Using Beanstalk "swap URLs" when done with the environment 
    ![](images/aim7.jpg)
    