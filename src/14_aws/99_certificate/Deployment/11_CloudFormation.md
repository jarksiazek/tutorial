### Q1
* Company has a cloudformation template that is used to create a huge list of resources.  
Which of the following should be considered when designing such Cloudformation templates? 
* Ensure to create one entire stack from the template
* **Look towards breaking the templates into smaller manageable templates**
    * use small components and create dedicated templates for them
* Package the template together and use the cloudformation deploy command
* Package the template together and use the cloudformation package command

### Q2
You have YAML file given to you which required to deploy a Lambda function.
Which of the following is required to ensure the deployment can take place? (select 2)
* **use the cloudformation package command to package the deployment**  
* use the cloudformation package command to deploy the deployment
* **Place the function code at the root level of the working directory along with YAML file**
    * https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-getting-started-hello-world.html
* Place the function code in the .eb extensions folder

