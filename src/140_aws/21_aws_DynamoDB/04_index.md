### Local Secondary Index ###
![](images/aim3.jpg)
* alternate range key for your table, local to hash key
* up to 5 local secondary indexes per table
* the sort key consists of exactly one scalar attribute
* the attribute must be a scalar String, Number or Binary
* LSI must be defined at table creation time

### Global Secondary Index ###
![](images/aim4.jpg)
* speed up queries on non-key attributes
* GSI = partition key + optional sort key
* the index is a new "table" and we can project attributes on it
    * the partition key and sort key of the original table are always projected (KEYS_ONLY)
    * can specify extra attributes to project (INCLUDE)    
    * or all attributes from main table (ALL)
* must define RCU/WCU for index 
* possible to add/modify GSI after creating original table
* if the writes are throttled on the GSI, then the main table will be throttled
* even if the WCU on the main table is fine
* choose partition key on GSI carefully 