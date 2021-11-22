A developer is writing a pp that will store data in DynamoDB table. The ratio of reads operations to write operations will be 1000 to 1, whith the same data being accessed frequently.   
What should the Developer enable on the DynamoDB table to optimize performance and minimize costs? 
* DynamoDB autoscaling
    * unpredicted workload
* DynamoDB cross-region replication
    * disaster recovery scenario 
* DynamoDB Streams
    * stream data to other sources
* **DynamoDB Accelerator**
    * DAX is a DynamoDB-compatible caching service that enables you to benefit from fast in-memory performance fo demanding applications DAX addresses three core scenarios: 
        * reduces the response times of eventually-consistent read workloads 
        * reduces operational and application complexity by providing a managed service that is API- compatible
        * for ready-heavy or bursty workload, DAX provides increased throughput and potential operational cost saving by reducing the need to over-provision read capacity units.  

