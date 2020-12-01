### Q1
You are developing an application that will be comprised of the following architecture
1) A set of EC2 instances to process the messages
2) These EC2 instances will be spun up by an Autoscaling group
3) SQS queues to maintain the processing messages
4) There will be 2 pricing tiers  
How will you ensure that the premium customers' messages are given more preferences? 
* Create 2 Autoscaling Groups, one for normal and one for premium customers
    * will still launch the same EC2 instances
* Create 2 sets of EC2 instances, one for normal and one for premium customers
    * launching 2 sets of EC2 instances involeves lots of manual work
* **Create 2 SQS queues, one for normal and one for premium customers**
    * best option - messages can then be processed by the application from the high priority queue first
    * https://aws.amazon.com/sqs/
* Create 2 Elastic Load Balancers, one for normal and one for premium customers**

### Q2
A developer is making use of AWS services to develop application. He has been asked to develop the application in a manner to compensate any network delays by implementing longer waits for nay error responses. 
Which of the following three mechanisms should he implemented in the application? (select 3)
* multiple SQS queues    
* **exponential backoff**
* **reties in your application code**    
* **consider using AWS SDK for Java**   
    * each AWS SDK implements exponential backoff 

