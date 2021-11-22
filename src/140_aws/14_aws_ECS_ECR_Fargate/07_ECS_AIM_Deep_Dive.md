### ECS IAM Roles ###
![](images/aim5.jpg)
* EC2 Instance Profile
    * Used by the ECS Agent
    * Makes API calls to ECS service
    * Send container logs to CloudWatch Logs
    * Pull Docker image from ECR
* ECS Task Role
    * Allow each task to have a specific role
    * Use different roles for the different ECS Services you run
    * Task Role is define in the **task definition**