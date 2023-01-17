### SSM - System Manager Overview
* EC2 and on-premises
* insights about the state 
* patching
* Windows and Linux
* Integrated with CloudWatch, AWS Config
* Free

### SSM Features
* Resource group 
  * logic grous created using tags
* Documents
  * written in JSON or yaml
  * parameters and actions
  * many AWS documents already exist
* SSM automation
  * simplifies common operations 
  * eg. restart instances, create an AMI, EBS snapshot etc
  * automation runbook - ssm documents of type automation
  * triggering
    * AWS Console, AWS CLI or SDK
    * EventBridge, AWS Config, Maintenance Windows    
