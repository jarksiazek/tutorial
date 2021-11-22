### PUB/SUB Pattern
![](images/aim11.jpg)
* helping send a message to many receivers

### Amazon SNS ###
* send messages to many dedicated consumers
* each subscriber to the topic will get all the messages (new feature to filter messages)
* up to 10 mlm subscribers per topic
* 100000 topics limit
* subscribers can be: 
    * SQS 
    * HTTP/HTTPS backend
    * lambda
    * emails 
    * SMS messages 
    * mobile notification
* integration with SNS
    * many service can send data directly SNS for notification
        * CloudWatch (for alarms)
        * Autoscaling group for notification
        * Amazon S3 (on bucket event)
        * CloudFormation (upon state changes, failed to build)
        * etc...

 ### Amazon SNS How Works ###
* topic publish (using SDK)
    * create topic 
    * create a subscription
    * publish topic
* direct publish (mobile SDk)
    * create platform application
    * create a platform endpoint
    * publish to platform endpoint
    * works with Google GCM, Apple APNS, Amazon ADM

### Amazon SNS - security ###
* encryption 
    * in-flight encryption using HTTPS API
    * at-rest encryption using KMS keys
    * client-side encryption - encryption/decryption on client 
* access control
    * IAM policy to regulate access to the SNS API
* SQS Access Policy
    * similar to S3 bucket policy
    * useful for cross-account access to SQS queue
    * useful for allowing other services (SNS, S3) to write an SNS topic 