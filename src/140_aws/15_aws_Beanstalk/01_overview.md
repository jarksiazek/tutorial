### Beanstalk ###
* End-to-end web application management
* deploying application in right way
* platform as service
* developer centric view of deploying an application on AWS         
* it uses all component's : EC2, ASG, ELB, RDS, etc...
* full control over configuration
* is free, but you pay for the underlying instances

### Elastic Beanstalk ###
* **Managed service**
    * instance configuration/ OS is handled by Beanstalk
    * deployment strategy is configurable but performed by Elastic Beanstalk
    
* just the application code is the responsibility of the developer

* **Tree architecture models**  
    * single instance deployment: good for dev
    * LB(load balancer) + ASG(auto-scaling group) great for production or pre-production web applications
    * ASG only: great for non-web apps in production (workers, etc...)
    
### Elastic Beanstalk - Components ###
* Elastic Beanstalk has three components
    * Application
    * Application version: each deployment gets assigned a version
    * Environment name (dev, test, prod...): free naming
    
* deploy application version to environments and can promote application version to the next environment
* rollback feature to previous application version
* full control over lifecycle of environment
![](images/aim1.jpg)
     
### Elastic Beanstalk - Languages ###
* Supports many platforms:
    * Go, Java SE, Java with Tomcat, .NET on Windows Server with IIS, Node.js, PHP, Python, Ruby, Packer Builder
    * Single Container Docker, Multicontrainer Docker, Preconfigured Docker
    * your custom platform (advanced)
    