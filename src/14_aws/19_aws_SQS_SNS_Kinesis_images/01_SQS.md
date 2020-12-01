### Queue
![](images/aim3.jpg)
* producers - generate message
* consumer - process data and removing it from the queue 

### Amazon SQS ###
* queue service
* producer -> queue -> consumer
* old service - 10 yrs
* fully managed service used to *decouple applications* 
* decoupling service
* Attributes
    * unlimited throughput, unlimited number of messages in queue
    * default retention of messages: 4 days, maximum of 14 days
    * low latency - <10ms on publish and receive
    * limitation 256 kb per message sent
    * can have duplicate messages (at least once delivery, occasionally)
    * can have out of order messages (best effort ordering)
    
### Amazon SQS - producing message ###
* produced to SQS using SDK (SendMessage API)
* the message will be **persisted** in SQS until a consumer reads message and deletes it
* message retention 1 second -14 days, default 4 days
* example: send an order to be processed
    * order id
    * customer id 
    * any attributes you want to

### Amazon SQS - consuming message ###
![](images/aim4.jpg)
* Consumers running on:
    * EC2 instances
    * Lambda
    * on-premises servers
* Poll SQS messages (receive up 10 messages at a time)
* Then processes the message (ex. write something in a database)
* Then deletes message in SQS using DeleteMessage API


### Amazon SQS - multi SQS consumers ###
![](images/aim5.jpg)
* consumers receive and process messages in parallel
* At least one delivery
* best-effort message ordering
* consumers delete message in SQS queue after delivering 
* we can scale consumers horizontally to improve throughput of processing -ASG

### Amazon SQS - ASG ###
![](images/aim6.jpg)
*  CloudWatch Metrics - Queue length - ApproximateNumberMessages

### Amazon SQS - decouple applications ###
![](images/aim7.jpg)
* you can scale producers and consumers independently

### Amazon SQS - security ###
* encryption 
    * in-flight encryption using HTTPS API
    * at-rest encryption using KMS keys
    * client-side encryption - encryption/decryption on client 
* access control
    * IAM policy to regulate access to the SQS API
* SQS Access Policy
    * similar to S3 bucket policy
    * useful for cross-account access to SQS queue
    * useful for allowing other services (SNS, S3) to write an SQS queue 

### Amazon SQS - Message Visibility Timeout ###
![](images/aim8.jpg)
* after a message is polled by consumer, is becomes invisible to other consumers
* by default - message visibility timeout is 30 seconds
* that means the message has 30 seconds to be processed
* after the message visibility timeout is over, the message is visible in SQS
* if a message is not processed within the visibility timeout, it will be processed twice potentially
* to get more time a consumer can change visibility using **ChangeMessageVisibility** API
* if visibility timeout is high(1 hour), and consumer crashes, re-producing will take time
* if visibility timeout is low(1 second), and consumer can get it twice

### Amazon SQS - Dead letter queue ###
* if a consumer fails to process the message with in VisibilityTimeout, message back to queue
* dead letter queue - threshold how many time the message can back to the queue
* MaximumReceive threshold - can break the loop from Dead letter queue (DLQ)
* when DLQ appears then the message should be sent to separate queue 

### Amazon SQS - Delay queue ###
* Custom setting to delay message to consumer
* default is 0, max is 15 mins
* can set a default at queue level
* can override the default on send using Delay/Seconds parameter

### Amazon SQS - Long polling ###
* consumer can wait for a message to arrive if there are none in the queue
* long polling decrease the number of API calls made to SQS while increasing the efficiency and latency of your app
* 1 sec to 20 sec (20 is preferable)
* Long polling is preferable to short polling
* can be enabled at the queue level or at the API level using WaitTimeSeconds
    
### Amazon SQS - extended client ##    
![](images/aim9.jpg)
* sending message bigger that 256KB
* use the SQS Extended Client (Java library)
* message will use S3 bucket to sent and poll message

### Amazon SQS - API ###
* CreateQueue, DeleteQueue
* PurgeQueue
* SendMessage (DelaySeconds) , ReceiveMessage, DeleteMessage
* ReceiveMessageWaitTimeSeconds - Long polling
* ChangeVisibilityTimeOut
* Batch Apis for helps decrease cost - SendMessage, DeleteMessage, ChangeVisibilityTimeout