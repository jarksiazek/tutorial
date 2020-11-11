### Messaging ###
* share information between services
* 2 patterns 
    * synchronous 
        * can be problematic if there are sudden spikes of traffic 
        * in that case is it better to decouple your application
            * using SQS - queue model
            * using SNS - pub/sub model
            * using Kinesis - real-time steaming model
    * asynchronous/ event based - middleware (queue)
    
### Amazon SQS ###
* queue service
* producer -> queue -> consumer
* old service - 10 yrs
* fully managed service used to decouple applications 
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
* the message will be persisted in SQS until a consumer reads message and deletes it
* message retention 1 second -14 days, default 4 days

### Amazon SQS - consuming message ###
* Consumers running on EC2 instances, on-premises servers or AWS Lambda
* Poll SQS messages (receive up 10 messages at a time)
* Then processes the message (ex. write something in a database)
* Then deletes message in SQS using DeleteMessage API

### Amazon SQS - multi SQS consumers ###
* consumers receive and process messages in parallel
* At least one delivery
* best-effort message ordering
* consumers delete message in SQS queue after delivering 
* we can scale consumers horizontally to improve throughput of processing -ASG

### Amazon SQS - ASG ###
*  CloudWatch Metrics - Queue length - ApproximateNumberMessages

### Amazon SQS - decouple applications ###
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
* after a message is polled by consumer, is becomes invisible to other consumers
* by default - message visibility timeout is 30 seconds
* that means the message has 30 seconds to be processed
* after the message visibility timeout is over, the message is visible in SQS
* if a message is not processed within the visibility timeout, it will be processed twice potentially
* to get more time a consumer can change visibility using ChangeMessageVisibility API
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

### Amazon SQS - advance ###
* Long polling
    * consumer can wait for a message to arrive if there are none in the queue
    * long polling decrease the number of API calls made to SQS while increasing the efficiency and latency of your app
    * 1 sec to 20 sec (20 is preferable)
    * Long polling is preferable to short polling
    * can be enabled at the queue level or at the API level using WaitTimeSeconds
* SQS extended client
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
 
 ### Amazon SQS - FIFO ###
* First In First Out
* limited throughput 300msg/sec without batching, 3000 msg/sec with batching
* exact one send capability (by removing duplicates)
* messages will be processed in order by consumer 
* deduplication
    * interval is 5 mins - if the same message will be sent twice in 5 minute period, the second one will be removed
    * two de-duplication methods:
        * content-based deduplication - will do a SHA-256 hash of the message body  
        * explicitly provide a message duplication ID
* message grouping
    * if you specify the same value of MessageGroupId is SQS FIFO, you can only have one consumer
    * to get ordering at the level of a subset of messages, specify different values for MessageGroupId
        * Message Group Id will be in order within the group
        * each Group Id will have different consumer (parallel processing)
        * ordering across groups in not guaranteed

 ### Amazon SNS ###
* send messages to many dedicated consumers
* each subscriber to the topic will get all the messages (new feature to filter messages)
* up to 10 mlm subscribers per topic
* 100000 topics limit
* subscribers can be: SQS, HTTP/HTTPS backend, lambda, emails, SMS messages, mobile notification
* integration with SNS
    * many service can send data directly SNS for notification
    * CloudWatch (for alarms)
    * Autoscaling group for notification
    * Amazon S3 (on bucket event)
    * CloudFormation (upon state changes, failed to build)

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
    
### Amazon SNS + SQS - Fan out pattern ###
* push one message in SNS, receive in all SQS queues that are subscribed
* full decoupled, no data loss
* SQS allows for: data persistence, delayed processing and retries of work
* ability to add more SQS subscribers over time
* make sure your SQS queue access policy allows for SNS to write
* SNS cannot send messages to SQS FIFO (AWS limitation)
   
### Amazon Kinesis ###
* Kinesis is managed alternative to Apache Kafka
* Big data streaming tool
* Great for application logs, metrics, IoT, clickstream
* Great for real time big data 
* Great for streaming processing framework(Spark, NiFi, etc...)
* Data is automatically replicated to 3 AZ

### Amazon Kinesis Products ###
![](.19_aws_SQS_SNS_Kinesis_images/aim1.jpg)
* Kinesis streams: low latency streaming ingest at scale
* Kinesis Analytics: perform real-time analytics on streams using SQL
* Kinesis Firehose: lead streams into S3, Redshift, ElasticSearch

### Amazon Kinesis Streams ###
* Steams are divided in ordered Shards/Partitions
![](.19_aws_SQS_SNS_Kinesis_images/aim2.jpg)
* Data retaintion is 1 day by default can go up to 7 days
* Kinesis is massive pipe/highway of data
* Ability to reprocess/ replay data
* multiple applications can consume the same stream 
* real-time processing with scale of throughput
* once data is inserted in Kinesis, it can't be deleted (immutability)
* Kinesis streams shards:
    * one stream is made of many shards
    * one shard write is 1 MB/s or 100 messages/s    
    * one shard read is 2 MB/s
    * billing is per shared provisioned, can have as many shards as you want
    * batching availability or per message calls
    * the number of shards can evolve over time (reshard/merge)
    * records will be ordered per shard 
* Kinesis - producer API
    * PutRecords API + Partition key that gets hashed
    * the same key goes to the same partition (helps with ordering for a specific key)
    * message sent get a "sequence number"
    * choose a partition key that is highly distributed (helps prevent "hot parition")
        * user_id if many users (great key)
        * NOT country_id if 90% of the users are in one country
    * use batching with PutRecords to reduce cost and increase throughput
    * ProvisionedThroughputException if we go over the limits
    * can use CLI AWS SDK or producer libraries from various frameworks
* Kinesis - producer Exceptions
    * ProvisionedThroughputException 
        * to much data (exceeding MB/s or TPS for any shard)
        * potential hot shards (bad partition key)
    * Solution
        * Reties with backoff
        * increase shards
        * check partition key - message distribution
* Kinesis - consumer API
    * can use normal consumer CLI, SDK, ect...
    * can use Kinesis Client Library (Java, Node, Python, Ruby, .Net)
        * KCL can use  DynamoDB to checkpoint offsets 
        * KCL uses DynamoDB to track other workers and share the work amongst shards
        
### Amazon Kinesis KCL ###
* Kinesis Client Library (KCL) - Java library that helps read from a Kinesis Streams with distributed applications sharing the read workload
* Rule: each shard is be read by only one KCL instance
    * Means 4 shards = max 4 KCL instances
    * progress is checkpointed into DynamoDB (need IAM access)
    * KCL can run on EC2, Elastic Beanstalk, on Premise Application
    * records are read in order at shard level
    
### Amazon Kinesis Security ###
* Control access/ authorization using IAM policies
* encryption in flight using HTTPS endpoints
* encryption at rest using KMS
* possibility to encrypt/decrypt data client side
* VPC endpoints available for Kinesis to access with VPC

### Amazon Kinesis Analytics ###
* perform real-time analytics on Kinesis Steams using SQL
* Kinesis Data Analytics: 
    * Auto scaling
    * Managed: no servers to provision
    * continuous: real time
* pay for actual consumption rate
* can create streams out of the real-time queries 

### Amazon Kinesis Firehose ###
* fully managed service
* near real time (60 sec latency)
* load data into Redshift/Amazon S3/ ElasticSearch/ Splunk
* automatic scaling
* support many data format ( pay for conversion)
* pay for the amount of data going through Firehose

### SQS SNS KINESIS
* SQS 
    * consumer poll data
    * data is deleted after being consumed
    * many consumers as you want
    * no need to provision throughput
    * no ordering (except FIFO)
    * individual message delay capability
* SNS 
    * push data to many subscribers
    * up to 10 mln subscribers
    * data is not persisted (lost if not delivered)
    * Pub/sub 
    * up to 100000 topics
    * no need to provision throughput
    * integrates with SQS for fanout architecture pattern
* Kinesis
    * consumers "pull data"
    * many consumers as we need
    * one consumer per shard
    * possibility to replay data
    * meant for real-time big data, analytics and ETL 
    * ordering at the shard level
    * data expires after x days
    * must provision throughput

### Ordering Data Kinesis
* using partition key for example truck_id
* the same partition key will always go to the same shard

        
         
 
  
    





    
    
   
        



  



    


  
    
    
    

         

      