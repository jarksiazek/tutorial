### ECS - Service Auto Scaling ###
* CPU and RAM are tracked in CloudWatch at the EXC service level
* Target Tracking: target a specific average CloudWatch metric
* Step Scaling: scale based on CloudWatch alarms
* Scheduled Scaling: based on predictable changes

* **ECS Service Scaling (task level) not equal EC2 Auto Scaling (instance level)** 

### ECS - Service Auto Scaling Fargate ###
* Fargate Auto Scaling is much easier to set up (because serverless)

### Cluster Capacity Provider
![](images/aim7.jpg)
* is used in association with a cluster to determine the infrastructure that a task runs on 
    * for ECS and Fargate users, the FARGET and FARGET_SPOT capacity providers are added automatically
    * for ECS on EC2, you need to associate the capacity provider with an  auto-scaling group