### Free Tier ###
Free tier - 12 months free access
https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc

* encryption at rest 
    * is vital for regulatory compliance to ensure that sensitive data saved on disks is not readable by any user or application without a valid key
* encryption in flight
    * using HTTPS endpoints

### Basic Services ### 
Service | Full-name |  Description | Pricing 
--- | --- | --- | ---
VPC | Virtual Private Cloud | isolated section of the Amazon Web Services | free
NGW | NAT Gateway |  VPC component that allows communication between your VPC and the internet | free  
EC2 | Amazon Elastic Compute Cloud | compute capacity in the cloud | cost per hour, varies base on (region, instance type, on-demand, spot, reserved, dedicated host, operating system linux/Windows), you are billed by the second with minimum of 60 seconds, you are billed for storage, data transfer, fixed public IP, load balancing, not pay when instance is stopped
EBS | Elastic Block Stock | Network drive you can attach to instances in one AZ | per GB-month
EFS | Elastic File System | NFS can be mounted on many EC2 in one region | per GB-month
ELB | Elastic Load Balancer | Load Balancer | free, pay for resources (EC2)
S3 | S3 | infinitely scaling storage  | per GB-month, data transfer
S3 Glacier| S3 Glacier |secure, durable, and extremely low-cost Amazon S3 cloud storage | GB-month
ECS | Elastic Container Service | Container Managed Service | 
ECR | Elastic Container Registry | 
Fargate |
Beanstalk | Elastic Beanstalk | developer centric view of deploying | free, pay for resources
CloudFormation | CloudFormation | Infrastructure as Code | service is free, pay for resources      
DynamoDB | DynamoDB | NoSQL serverless database |  write and read, data storage GB-month
   