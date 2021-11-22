### ElastiCache ###
* The same way RDS is to get managed Relational Databases
* ElasticCache is to get managed Redis or Memcached
* Caches are in-memory databases with really high performance, low latency
* helps reduce load off of databases for read intensive workloads
* helps make your application stateless
* write scaling using sharding (horizontal partition of data)
* read scaling using Read Replicas
* Multi AZ with Failover Capability
* AWS takes care of OS maintenance, patching, optimizations, setup, configuration, monitoring, failure recovery and backups

### ElasticCache Solution Architecture ###
* DB Cache
    * application queries ElasticCache, if not available, get from RDS and store in ElasticCache  
    * helps relieve load in RDS
    * cache must have an invalidation strategy to make sure only the most current data is used in there
* user session store
    * user logs into any of the application
    * the application writes the session data into ElasticCache
    * the user hits another instance of our application  
    * the instance retrieves the data and user is already logged in

### ElasticCache Redis vs Memcached ###
* Redis
    * Multi AZ with Auto-Failover
    * Read Replicas to scale reads and have high availability
    * Data Durability using AOF persistence (save data after stopping redis) 
    * Backup and restore features
    * similar to RDS 
* Memcached
    * Multi-node for partitioning of data (sharding)
    * non persistent - lives only in memory
    * no backup and restore
    * multi-threaded architecture
    
### ElasticCache Strategies  ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/15300184#content
* https://aws.amazon.com/caching/implementation-considerations    
* Not for every data,  data may be out of date, eventually consistent
* Caching types
    * Lazy Loading/ Cache-Aside / Lazy Population
 ![](images/aim3.jpg) 
        - pros
            * only requested data is cached (the cache isn't filled up with unused data)
            * node failures are not fatal (just increased latency to warm the cache) 
        - cons
            * cache miss penalty that results in 3 round trips, noticeable delay for that request     
            * stale data: data can be updated in the database and outdated in the cache 
    * Write Though 
        * Add or Update cache when database is updated
         ![](images/aim4.jpg) 
        - pros
            * data in cache is never stale, reads are quick
            * write penalty vs read penalty (each write requires 2 write calls - db and cache) 
        - cons
            * missing data until it is added/updated in the DB, Migration is to implement Lazy Loading strategy as well         
            * cache churn - a lot of the data will never be read   
            
* Cache Evictions and Time-to-live (TTL)
    * cache eviction can occur in the ways:
        * delete item explicitly
        * cache is full and item isn't used recently (LRU)
        * set TTL