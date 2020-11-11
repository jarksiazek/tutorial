### ECS ###
* Docker containers in AWS

### DOCKER ###
* is a software development platform to deploy apps
* apps are packaged in containers that can be run on any OS
* apps run the same, regardless of where they're run
    * any machine
    * no compatibility issue
    * predictable behaviour
    * less work
    * easier to maintain and deploy
    * run docker container on EC2
* storing docker images
    * public:dockerhub
    * private: Amazon ECR (Elastic Container Registry)
* docker vs virtual machines
![](.14_aws_ECS_images/aim1.jpg)
    * docker is "sorf of" a virtualization technology, but not exactly
    * resources are shared with the host => many container on one server
    * lighter than vm 
* docker containers management 
    * container management platform
        * ECS: Amazon's own platform
        * Fargate: Amazon's own Serverless platform
        * EKS: Amazon;s managed Kuberneter (open source)
      
### ECS Clusters ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/13495746#overview
* ECS Clusters are logical grouping of EC2 instances
* EC2 instances run the ECS agent (Docker container)
* the ECS agents registers the instance to the ECS cluster
* EC2 instances run a special AMI,made specifically for ECS

### ECS Task Definition ###
* metadata in JSON form to tell ECS how to run a Docker Container
* contains crucial information:
    * image name 
    * port binding for a container to host
    * memory and CPU required 
    * environment variables
    * networking information

### ECS Service ###
* helps define how many tasks should tun and how they should be run
* they ensure that the number of tasks desired is running across our fleet of EC2 instances
* they can be linked to ELB / NLB / ALB (load balancers) if needed  

### ECS Service with Load Balancer ###
* https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/13495758#content           

### ECR ###
* Elastic Container Registry
* private docker image repository
* access is controlled through IAM (permission errors => policy)  
* AWS CLI v1 login command (may be asked at the exam)
```bash 
$(aws ecr get-login --no-include-email region eu-west-1)    
```
* AWS CLI v2 login command
```bash 
aws ecr get-login-password region eu-west-1 | docker login --username AWS --password-stdin 12qweq.dkr.amazon.com    
```
* Docker push & pull:
    * docker push 1212.dfde.eu-west-1.amazonaws.com/demo:latest
    * docker pull 1212.dfde.eu-west-1.amazonaws.com/demo:latest
    
### Fargate ###
 * just create definitions, and AWS will run our containers for us
 * it's serverless
 * simpler version of ECS, better scaling
 
 ### ECS Task Placement ###
* when a task of type EC2 is launched ECS must determine where to place it, with the constraints of CPU,memory, port
* similarly, when a service scales in, ECS needs to determine which task terminate
* to assist with this, you can define a task placement strategy and task placement constraints 
* this is only for ECS with EC2, not for fargate  
* ECS Task Placement Strategies
    * Binpack
        * place tasks based on the least available amount of CPU or memory
        * this minimizes the number of instances in use (cost saving)
    * Random
        * place the task randomly
    * Spread
        * place the task evenly based on the specified value
        * example: instanceId, attribute.availability-zone
* ECS Task Placement Constraints
    * distinctInstance: place each task on a different container instance
    * memberOf: places task on instance that satisfy an expression
        * uses the Cluster Query Language (advanced)
    
### ECS - Service Auto Scaling ###
* CPU and RAM are tracked in CloudWatch at the EXC service level
* Target Tracking: target a specific average CloudWatch metric
* Step Scaling: scale based on CloudWatch alarms
* Scheduled Scaling: based on predictable changes
* ECS Service Scaling (task level) not equal EC2 Auto Scaling (instance level) 
* Fargate Auto Scaling is much easier to set up (because serverless)
* Cluster Capacity Provider
    * is used in association with a cluster to determine the infrastructure that a task runs on 
        * for ECS and Fargate users, the FARGET and FARGET_SPOT capacity providers are added automatically
        * for Amazon ECS on EC2, you need to associate the capacity provider with an  auto-scaling group
        
        
### ECS Tips for Exam # 
*  ECS is to run Docker containers and has 3 flavors:
    * ECS Classic EC2 instance to run container
        * EC2 instance must be created
        * we must configure the file /etc/ecs/ecs.config with the cluster name
        * ECS instance must run an ECS agent
        * EC2 instances can run multiple containers on the same type
            * host port(dynamic) cannot be specified, only container port
            * should use an Application Load Balancer with dynamic port mapping
            * EC2 instance security group must allow traffic from the ALB on all ports
            * Security groups operate at the instance level, not task level
        * ECS tasks can have IAM Roles to execute actions agains AWS     
    * Fargate: ECS Serverless, no EC2
        * serverless
        * AWS provisions container for us and assigns them ENI (Elastic Network Interface)
        * Fargate containers are provisioned by the container spec (CPU/RAM)
        * Fargate tasks can have IAM Roles to execute actions against AWS        
    * EKS: Managed Kubernetes by AWS
* ECR 
    * is tightly integrated with IAM 
    * 2 log in options 
        * AWS CLI v1 login command
        * AWS CLI v2 login command with pipe   
* ECS OTHER
    * ECS does integrate with Cloud Watch Logs
        * you need to set up logging at the task definition level
        * each container will have a different log stream
        * each EC2 Instance Profile needs to have the correct AIM permission 
    * Use IAM Task Roles for your tasks 
    * Task Placement Strategies: binpack, random, spread
    * Service Auto Scaling with target tracking, step scaling or scheduled
    * Cluster Auto Scaling through Capacity Providers
        