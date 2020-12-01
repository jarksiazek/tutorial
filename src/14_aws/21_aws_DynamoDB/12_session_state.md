### DynamoDB Session State Cache
* it's common to use DynamoDB to store session state
* vs ElasticCache  
    * ElasticCache is in-memory, by DynamoDB is serverless
    * both key/value store
* vs EFS (Elastic File System)
    * EFS must be attached to EC2 as a network drive
* vs EBS & Instance Store
    * EBS & Instance Store can only be used for local caching, not shared caching
* vs S3
    * S3 is higher latency and not meant for small objects



