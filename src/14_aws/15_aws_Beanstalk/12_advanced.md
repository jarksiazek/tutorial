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
    ![](images/aim9.jpg)

### Custom Platform
* allows defining custom platform
    * the operating system   
    * additional software
    * scripts that Beanstalk runs on these platforms
* use case: app language is incompatible with Beanstalk and doesn't use Docker     
* to create own platform
    * define an AMI using platform.yaml    
    * build that platform using the Packer software (open source tool to create AMIs)
* Custom Platform vs Custom Image (AMI)
    * Custom Image is to tweak an existing Beanstalk Platform (Python, Node, Java) 
    * Custom Platform is to create an  entirely new Beanstalk Platform 