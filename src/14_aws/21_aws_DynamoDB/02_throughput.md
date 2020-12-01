### Provisioned Throughput ###
* table must have provisioned read and write capacity units
* **Read Capacity Units (RCU)** - throughput for reads
* **Write Capacity Units (WCU)** - throughput for writes
* option to setup auto-scaling of throughput to meet demand
* throughput can be exceeded temporarily using "burst credit"
* if burst credit are empty, you'll get a "ProvisionedThroughputException"
* it's then advised to do an exponential back-off retry

### Write Capacity Units ###
* *1 WCU* represents one write per second for an item up to 1kb in size
* if the items are larger that 1 kb, more WCU are consumed

### Read Capacity Units ###
* *1 RCU* represents 1 strongly consistent read per second, or 2 eventually reads per second with size 4 kb
* if the items are larger that 4 kb, more WCU are consumed

### Strongly Consistent Read vs Eventually Consistent Read
* Eventually Consistent Read (default): 
    * if we read just after a write, it's possible we'll get unexpected response because of replication
* Strongly Consistent Read (option):
    * if we read just after a write, we get the correct data
* by default: DynamoDB uses **Eventually Consistent Read**, but GetItem, Query and Scan provide a "ConsistentRead" parameter you can set it to True        

### DynamoDB - Partitions Internal
* data is divided in partitions
* partition keys go through a hashing algorithm to know to which partition they go to 
* to compute the number of partitions
    * by capacity (TOTAL RCU/3000) + (TOTAL WCU/1000)
    * by size - 10GB
    * total partitions (CEILING(MAX(Capacity,Size)))

### DynamoDB - Throttling
* if we exceed our RCU or WCU we get ProvisionedThroughputExceededExceptions
* reasons:
    * hot key: one partition key is being read too many times (popular item for ex)
    * hot partitions : very large item
* solution:
    * exponential back-off
    * distribute partition keys as much as possible
    * if RCU issue, we can use DynamoDB Accelerator (DAX)
     
    
