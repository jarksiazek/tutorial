### ECS Task Placement ###
![](images/aim6.jpg)
* when a task of type EC2 is launched ECS must determine where to place it, with the constraints of CPU,memory, port
* similarly, when a service scales in, ECS needs to determine which task terminate
* to assist with this, you can define a task placement strategy and task placement constraints 
* this is only for ECS with EC2, not for fargate  

### ECS Task Placement Process
* Task placement strategies are a best effort
* When ECS places tasks, it uses the following process to select container instances:
    1) Identify the instances that satisfy the CPU, memory and port requirement in the task definition
    2) Identify the instances that satisfy the task placement constraints
    3) Identify the instances that satisfy the task placement strategies  
    4) Select the instances for task placement

### ECS Task Placement Strategies
* Binpack
    * place tasks based on the least available amount of CPU or memory
    * this minimizes the number of instances in use (cost saving)
* Random
    * place the task randomly
* Spread
    * place the task evenly based on the specified value
    * example: instanceId, attribute.availability-zone
The can mix together: ex. binpack + spread

### ECS Task Placement Constraints
* distinctInstance: place each task on a different container instance
* memberOf: places task on instance that satisfy an expression
    * uses the Cluster Query Language (advanced)