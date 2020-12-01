### Elastic Beanstalk Lifecycle Policy ###
* Elastic Beanstalk can store at most 1000 application versions
* to phase out old application versions, use a **lifecycle policy**
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
    ![](15_aws_Beanstalk/aim8.jpg)

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
    ![](15_aws_Beanstalk/aim9.jpg)


    
    