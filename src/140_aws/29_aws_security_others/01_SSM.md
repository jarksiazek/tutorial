### SSM Parameter Store ###
![](images/aim1.jpg)
* secure storage for a configuration and secrets 
* optional seamless encryption using KMS
* serverless, scalable, durable, easy SDK
* version tracking of configurations/ secrets
* configuration management using path and IAM
* notification with CloudWatch Events 
* integration with CloudFormation

### SSM Standard vs Advanced ###
Feature | Standard |  Advanced 
--- | --- | ---
number of parameters | 10000 | 100000
max parameter size | 4kb | 8kb
parameter policies available | No | Yes
cost | free | charges apply
storage pricing | free | $0.05 advanced parameter/month
API Interaction | Standard throughput : free, higher: $0.05 per 100000 | standard and higher $0.05 per 100000 

### Parameter Policies (advanced parameters)
* TTL to force updating or deleting sensitive data such as passwords
* can assign multiple policies at a time
