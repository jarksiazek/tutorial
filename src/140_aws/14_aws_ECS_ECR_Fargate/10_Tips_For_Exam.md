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
        * ECS tasks can have IAM Roles to execute actions against AWS     
        * Security groups operate at the instance level, not task level
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
        