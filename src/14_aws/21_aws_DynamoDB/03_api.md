### Writing Data ###
* PutItem - write data to DynamoDB (create or full replacement)
    * consume WCU
* UpdateItem - update data (partial update of attributes)
    * possibility to use Atomic Counter and increase them 
* Conditional Writes
    * accept a write/update only if conditions are respected, otherwise reject
    * helps with concurrent access to items
    * no performance impact
 
### Deleting Data ###   
 * DeleteItem 
    * delete individual row
    * ability to perform a conditional delete
* DeleteTable   
    * delete a whole table and all its items
    * much quicker deletion than calling DeleteItem on all items
 
### Batching Data ###   
* BatchWriteItem
    * up to 15 PutItem and/or DeleteItem in one call
    * up to 16MB of data written
    * up to 400kb of data per item
    * allows saving in latency by reducing the number of API calls done against DynamoDB 
    * operations are done in parallel for better efficiency
    * it is possible for part of batch to fail, in which case we have the try the failed items (exponential back-off)

### Reading Data ###   
* GetItem
    * Read based on Primary key
    * Primary Key = HASH or HASH-RANGE
    * Eventually Consistent read by default
    * option to use strongly consistent read
    * **ProjectionExpression** can be specified to include only certain attributes
* BatchGetItem
    * up to 100 items
    * up to 16 MB of data
    * items are retrieved in parallel to minimize latency

### Query Data ###   
* query returns items based on:
    * PartitionKey value (must be = operator)
    * SortKey value (=,<,>,between, begin) - optional
    * FilterExpression to further filter (client side filtering)
* returns:  
    * up to 1 MB of data
    * or number of items specified in limit
    * able to do pagination on the results
* can query table, a local secondary index or global secondary index
    
### Scan Data ###   
* scan the entire table and the filter out data (inefficient)
* returns up to 1MB of data - use pagination to keep on reading
* consumes a lot of RCU
* limit impact using Limit or reduce the size of the result and pause
* **parallel scan** - fast performance
* can use a ProjectionExpression + FilterExpression (no change to RCU)