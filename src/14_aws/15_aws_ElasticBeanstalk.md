### Beanstalk ###
* End-to-end web application management
* deploying application in right way
* platform as service
* developer centric view of deploying an application on AWS         
* it uses all component's : EC2, ASG, ELB, RDS, etc...
* full control over configuration
* is free but you pay for the underlying instances

### Elastic Beanstalk ###
* managed service
    * instance configuration/ OS is handled by Beanstalk
    * deployment strategy is configurable but performed by Elastic Beanstalk
* just the application code is the responsibility of the developer
* tree architecture models
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
![](.15_aws_Beanstalk_images/aim1.jpg)
     
### Elastic Beanstalk - Languages ###
* Supports many platforms:
    * Go, Java SE, Java with Tomcat, .NET on Windows Server with IIS, Node.js, PHP, Python, Ruby, Packer Builder
    * Single Container Docker, Multicontrainer Docker, Preconfigured Docker
    * your custom platform (advanced)
    
### Elastic Beanstalk Deployment Modes ###
* Single Instance - Great for dev
* High Availability with Load Balancer - Great for prod  
![](.15_aws_Beanstalk_images/aim2.jpg)

### Elastic Deployment Options for Updates ###
* All at once     
    * faster deployment 
    * application has downtime
    * great for quick iterations in development environment
    * no additional cost  
    ![](.15_aws_Beanstalk_images/aim3.jpg)
    
* Rolling 
    * application is running below capacity
    * can set bucket size
    * application is running both versions simultaneously
    * no additional cost 
    * long deployment   
    ![](.15_aws_Beanstalk_images/aim4.jpg)

* Rolling with additional batches 
    * application is running at capacity
    * can set the bucket size
    * small additional cost
    * additional batch is removed at the end of the deployment
    * long deployment
    * good for prod
    ![](.15_aws_Beanstalk_images/aim5.jpg)

* Immutable
    * zero downtime
    * new code is deployed to new instances on temporary ASG
    * high cost, double capacity
    * longest deployment
    * quick rollback in case of failures (just terminate new ASG)
    * great for prod  
    ![](.15_aws_Beanstalk_images/aim6.jpg)

* Blue/Green
    * Not a "direct failure" of Elastic Beanstalk
    * Zero downtime and release facility
    * create a new "stage" environment and deploy v2 there 
    * the new environment (green) can be validated independently and roll back if issues
    * Route 53 can be set up using weighted policies to redirect a little bit of traffic to stage environment
    * Using Beanstalk "swap URLs" when done with the environment 
    ![](.15_aws_Beanstalk_images/aim7.jpg)

### Elastic Beanstalk CLI ###
* install EB cli and work with Beanstalk from CLI 
* basic commands
    * eb create, eb status, eb health, eb events, eb logs, eb open, eb deploy, eb config, eb terminate 
    
### Elastic Beanstalk Deployment Process ###
* describe dependencies (requirements.txt for Python, package.json for Node.js)
* package code as zip and describe dependencies
    * Python: requirements.txt
    * Node.js package.json
* Console: upload zip file (create new app version), and then deploy
* Beanstalk will deploy the zip on each EC2 instance, resolve dependencies and start the application

### Elastic Beanstalk Lifecycle Policy ###
* Elastic Beanstalk can store at most 1000 application versions
* to phase out old application versions, use a lifecycle policy
    * based on time (old versions are removed)
    * based on space (when you have too many versions)
* versions that are currently used won't be deleted
* option not ot delete the source bundle in S3 to prevent data loss

### Elastic Beanstalk Extensions ###
* a zip file containing our code must be deployed to Elastic Beanstalk
* requirements 
    * in the .ebextensions/ directory in the root of source code
    * YAML/JSON format
    * .config extensions(example: logging.config)
    * able to modify some default setting using: option_settings
    * ability to add resources such as RDS, ElasticCache, DynamoDB, etc
    
### Elastic Beanstalk and CloudFormation ###
* under the hood, Beanstalk relies on CloudFormation
* CloudFormation is used to prevision other AWS services (we'll se later)

### Elastic Beanstalk Cloning ###
* clone an environment with the exact configuration
* use for deploying a "test" version of your application
* all resources and configuration are preserved: 
    * load balancer type and configuration
    * RDS database type (but the data is not preserved)
    * environment variables 
    
### Elastic Beanstalk Migration: Change Load Balancer Type ###
* after creating an Elastic Beanstalk environment, you cannot change the Load Balancer Type 
* to migrate and change LB
    1) create a new environment with same configuration except EB (can't clone)
    2) deploy your application onto the new environment
    3) perform a CNAME swap or Route 53 update
    
### RDS with Elastic Beanstalk ###
* RDS can be provisioned with Beanstalk, which is great for dev/test
* this is not great for prod as the database lifecycle is tied to the Bean environment lifecycle
* the best for prod is to separately create an RDS database and provide our EB application with the connection string

### Elastic Beanstalk Single Docker ###
* Run your application as single docker container
* Either provide:
    * Dockerfile: Elastic Beanstalk will build and run the Docker container
    * Dockerrun.aws.json(v1): Describe where *already built* Docker image is :
        * Image
        * Ports
        * Volumes
        * Logging, etc
* Beanstalk in Single Docker Container does not use ECS

### Elastic Beanstalk Multi Docker Container ###
* helps run multiple containers per EC2 instance in EB
* this will create for you: 
    * ECS Cluster
    * EC2 instances, configured to use the ECS
    * Load Balancer (in high availability mode)
    * task definitions and execution
* Dockerrun.aws.json(v2) at the root of the source code, will be used to generate ECS task definition
    ![](.15_aws_Beanstalk_images/aim8.jpg)

### Elastic Beanstalk and HTTPS ###
* Beanstalk with HTTPS
    * Idea: Load the SSL certificate onto the Load Balancer
    * can be done from the Console (EB console, load balancer configuration)
    * can be done from the code: .bextensions/securelisteners-alb.config    
    * SSL Certificate can be provisioned using ACM (AWS Certificate Manager) of CLI
    * Must configure a security group rule to allow incoming port 443(HTTPS port)
* Beanstalk redirect HTTP to HTTPS
    * configure your instances to redirect HTTP to HTTPS
    * OR configure the Aplication Load Balancer (ALB only) with a rule
    * make sure health checks are not redirected (so they keep giving 200 OK)
    
### Web Server vs Worker Environment ###
* if your application performs tasks that are long to complete, offload these tasks to a redictaed work environment 
* Decoupling your application into two tiers is common
* example: processing a video, generating a zip file, ect  
* you can define periodic tasks in a file cron.yaml
    ![](.15_aws_Beanstalk_images/aim9.jpg)


    
    