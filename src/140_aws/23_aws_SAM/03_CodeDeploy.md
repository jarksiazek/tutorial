### SAM and CodeDeploy ### 
* SAM Framework natively uses CodeDeploy to update Lambda function
    * Traffic Shifting feature
    * Pre and Post traffic hooks features to validate deployment (before the traffic shift starts and after it ends)
    * easy and automated rollback using CloudWatch Alarms
             