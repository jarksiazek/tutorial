### Q1
a developer has been asked to create an AWS Elastic Beanstalk environment for a production web app which needs to handle thousands of requests. Currently, the dev environment is running on t1.micro.  
What is the best way for a developer to provision a new production environment with a m4.large instead of t1? 
* Use CloudFormation to migrate the EC2 type from t1.micro to t4.large
* **Create a new configuration file with the instance type as m4.large and reference this file when provisioning the new environment.**
    * https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.managing.ec2.html
    * 
* Provision a m4.large instance directly in the dev environment and deploy to new production env
* Change the instance type value in the configurations file to m4.large by using the update autoscaling group CLI command 
 
### Q2
![](images/aim1.jpg)
An organization is using AWS Beanstalk for a web application. the developer needs to configure the Beanstalk envrionmoent with deployment methods that will create new instances and deploy code to those instances.  
Which methods will deploy code ONLY to new instances? (select 2)
* All at once deployment
* **Immutable deployment**
    * immutable update to lunch a full set of new instances 
* Rolling deployment
* Linear deployment
* **Blue/green deployment**

### Q3
You have benn instructed to manage the deployments of an application onto Elastic Beanstalk. Since this is just a development environment, you have told to ensure that the least amount of time is taken for each deployment.  
Which of the following deployment mechanism would you consider based on this requirement. 
* **all ay once**
    * is the least deployment option - the fastest 
* rolling
* immutable
* rolling with additional batch

