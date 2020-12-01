### Elastic Beanstalk Single Docker ###
* Run your application as single docker container
* Either provide:
    * **Dockerfile**: Elastic Beanstalk will build and run the Docker container
    * **Dockerrun.aws.json(v1)**: Describe where *already built* Docker image is :
        * Image
        * Ports
        * Volumes
        * Logging, etc
* Beanstalk in Single Docker Container **does not use ECS**

### Elastic Beanstalk Multi Docker Container ###
![](images/aim8.jpg)
* helps run multiple containers per EC2 instance in EB
* this will create for you: 
    * ECS Cluster
    * EC2 instances, configured to use the ECS
    * Load Balancer (in high availability mode)
    * task definitions and execution
* requeries a config **Dockerrun.aws.json(v2)** at the root of the source code     
* **Dockerrun.aws.json(v2)** will be used to generate **ECS task definition**
* your Docker images must be pre-built and stored in ECR