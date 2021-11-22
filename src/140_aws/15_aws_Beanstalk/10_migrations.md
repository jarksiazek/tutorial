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

### Elastic Beanstalk Migration: decouple RDS ###
1) create a snapshot of RDS DB (as a safeguard)
2) go to the RDS console and protect the RDS database form deletion
3) create a new Elastic Beanstalk environment, without RDS, point your application to existing RDS 
4) perform a CNAME swap or Route 53 update, confirm working
5) terminate the old environment (RDS won't be deleted)
6) Delete CloudFormation stack (in DELETE_FAILED state)
