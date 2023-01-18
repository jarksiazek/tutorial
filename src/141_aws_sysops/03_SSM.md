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
* SSM patch manager
  * automate patching process
  * os update, security etc.
  * EC2 and on-premises, Linux and Windows
  * patch on-demand or scheduled
  * generate patch report
  * Components
    * Patch Baseline
      * for all instances, critical, security updates 
    * Patch Group 
      * for groups defined by tags

* SSM session manager
  * allows to start secure shell on EC2 or on-premises
  * Linux and Windows
  * connection logs and executed commands are stored
  * session logs can be sent to S3 or CloudWatch
  * permission can be restricted to specific instances or even specific commends 
  * components
    * User (with permissions) -> Session manager -> (exec commends) ->  SSM Agent with permissions     

* OpsWork
  * Chef & Puppet 
