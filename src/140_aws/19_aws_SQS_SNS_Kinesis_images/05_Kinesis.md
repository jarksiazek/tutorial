### Amazon Kinesis ###
* Kinesis is managed alternative to Apache Kafka
* Big data streaming tool
* Great for application logs, metrics, IoT, clickstream
* Great for real time big data 
* Great for streaming processing framework(Spark, NiFi, etc...)
* Data is automatically replicated to 3 AZ

### Amazon Kinesis Products ###
* Kinesis streams: low latency streaming ingest at scale
* Kinesis Analytics: perform real-time analytics on streams using SQL
* Kinesis Firehose: lead streams into S3, Redshift, ElasticSearch

### Amazon Kinesis Together
![](images/aim1.jpg)

### Amazon Kinesis Streams ###
![](images/aim2.jpg)
* Steams are divided in ordered Shards/Partitions
* Data retaintion is 1 day by default can go up to 7 days
* Kinesis is massive pipe/highway of data
* Ability to reprocess/ replay data
* multiple applications can consume the same stream 
* real-time processing with scale of throughput
* once data is inserted in Kinesis, it can't be deleted (immutability)

### Amazon Kinesis Shards ###
* one stream is made of many shards
* one shard write is 1 MB/s or 100 messages/s    
* one shard read is 2 MB/s
* billing is per shared provisioned, can have as many shards as you want
* batching availability or per message calls
* the number of shards can evolve over time (reshard/merge)
* **records will be ordered per shard** 


### Kinesis - producer API
* PutRecords API + Partition key that gets hashed
* the same key goes to the same partition (helps with ordering for a specific key)
* message sent get a "sequence number"
* choose a partition key that is highly distributed (helps prevent "hot parition")
    * user_id if many users (great key)
    * NOT country_id if 90% of the users are in one country
* use batching with PutRecords to reduce cost and increase throughput
* ProvisionedThroughputException if we go over the limits
* can use CLI AWS SDK or producer libraries from various frameworks


### Kinesis - producer Exceptions
* ProvisionedThroughputException 
    * to much data (exceeding MB/s or TPS for any shard)
    * potential hot shards (bad partition key)
* Solution
    * Reties with backoff
    * increase shards
    * check partition key - message distribution        
        
### Kinesis - consumer API
* can use normal consumer CLI, SDK, ect...
* can use Kinesis Client Library (Java, Node, Python, Ruby, .Net)
    * KCL can use  DynamoDB to checkpoint offsets 
    * KCL uses DynamoDB to track other workers and share the work amongst shards
        
### Amazon Kinesis KCL ###
![](images/aim14.jpg)
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

        
         
 
  
    





    
    
   
        



  



    


  
    
    
    

         

      