### Elastic Beanstalk Cloning ###
* clone an environment with the exact configuration
* use for deploying a "test" version of your application
* all resources and configuration are preserved: 
    * load balancer type and configuration
    * RDS database type (but the data is not preserved)
    * environment variables 