### Concurrency
* DAX - DynamoDB Accelerator
* Seamless cache technology, no application re-write
* Writes go through DAX to DynamoDB
* Micro second latency for cached reads and query
* solves **hot key** problem (too many reads)
* 5 minutes TTL for cache by default
* option to have up to 10 nodes in the cluster
* multi AZ (3 nodes minimum recommended for production)
* secure (encryption at rest with KMS, VPC, IAM, CloudTrail...)

### DAX vs ElasticCache
* DAX 
    * individual objects cache 
    * Query/Scan cache
* ElasticCache
    * Stores aggregation results
 