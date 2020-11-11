### RDS  ###
* Relational Database Service
* database managed by AWS
    * Postgres
    * MySql
    * MariaDB
    * Oracle
    * Microsoft SQL Server
    * Aurora
* RDS service vs deploying DB on EC2
    * RDS managed service 
        * automated provisioning, OS patching
        * Continuous backups and restore a specific timestamp
        * monitoring dashboard to monitor db
        * read replicas for improved performance 
        * multi AZ setup for DR (Disaster Recovary)
        * Maintenance windows for upgrades
        * scaling capacity (vertical, horizontal)  
        * storage backed by EBS (gp2 or io1)
* RDS backups
    * automatically enabled in RDS
    * automated backups:
        * daily full backup of the db (during maintenance window)
        * transaction logs are backed-up EDS every 5 minutes
        * ability to restore to any point in time (from oldest backup to 5 minutes ago) 
        * 7 days retention (can be increased to 35 days)
* DB snapshots
    * manually triggered by the user
    * retention of backup for as long as you want

### RDS Read Replicas  ###
* helps to scale your reads 
* up to 5 replicas 
* within AZ, cross AZ or cross Region
* ASYNC replication so reads are eventually consistent (risk to have old data)
* Replicas can be promoted to their own DB
* applications must update the connection string to leverage read replicas
* read replicas are used for SELECT (=read) only kind of statements (not INSERT, UPDATE, DELETE)  
![](.07_aws_RDS_Aurora_ElastiCache_images/aim1.jpg) 
* Read Replicas - Network Cost
    * network cost when data goes from one AZ to another 
    * reduce cost keeping the Read Replicas in the same AZ - it's free

### RDS Multi AZ -DR (Disaster Recovery) ###
* SYNC replication
* failover in case of loss of AZ, loss of network, instance or storage failure
* The Read Replicas can be setup as Multi AZ for DR

### RDS Security - Encryption ###
* at rest encryption
    * Possibility to encrypt the master & read replicas with AWS KMS - AES-256 encyption
    * Encryption has to be defined at launch time
    * If the master is not encrypted, the read replicas cannot be encrypted
    * Transparent Data Encryption (TDE) available for Oracle and SQL Server
* in-flight encryption
    * SSL certificates to encrypt data to RDS in flight
    * provide SSL options with trust certificate when connecting to database
* RDS Encryption Operations
    * Encrypting RDS backups
        * snapshots of un-encrypted RDS database are un-encrypted
        * snapshots of encrypted RDS database are encrypted
        * can copy an un-encrypted snapshot into an encrypted one
    * Encrypt an un-encrypted RDS database
        * create a snapshot of the un-encrypted database  
        * copy the snapshot and enable encryption for the snapshot
        * restore the database from the encrypted snapshot
        * migrate applications to the new database, and delete the old database
* RDS Security - Network and IAM
    * RDS databases are usually deployed within a private subnet, not in public one
    * RDS security works by leveraging security groups (EC2 concept) - it controls which IP/security group can communicate with RDS 
    * IAM policies help control who can manage AWS RDS 
    * traditional username/password can be used to login into the database
    * RDS MySQL and PostgreSQL only - IAM-based authentication to login into db
        * you don't need password, just authentication token obtained through IAM and RDS API calls
        * token's lifetime only 15 minutes
        * benefits
            * network in/out must be encrypted using SSL 
            * IAM to centrally manage users instead of DB 
            * can leverage IAM Roles and EC@ Instance profiles for easy integration

### Aurora ###
* is not open source (AWS product)
* Postgres and MySQL are both supported as Aurora DB(your drivers will work as if Aurora was a Postres or MySQL database)
* cloud optimazed, claims 5x performance improvement over MySQL, 3x over Postgres
* automatically grows 10GB - 64TB
* 15 replicas (5 MySQL), replication process is faster (sub 10 ms replica lag)
* failover in Aurora is instantaneous. It's HA native.    
* costs more than RDS (20% more) - but is more efficient
* restore any point of time 
* high availability 
    * 6 copies of your data across 3 AZ
        * 4 copies out of 6 needed for writes 
        * 3 copies out of 6 need for reads 
        * self healing with peer-to-peer replication
        * storage is striped across 100s of volumes
    * one master Aurora instance takes writes     
    * automated failover for master in less than 30 seconds
    * master + up to 15 Aurora Read Replicas serve reads
    * support for Cross Region Replication
        * autoscaling option
        * reader endpoint - connection load balancing 
![](.07_aws_RDS_Aurora_ElastiCache_images/aim2.jpg) 
* security
    * similar to RDS (same engines)
    * encryption at rest using KMS
    * automated backups, snapshot and replicas are also encryped
    * Encryption in flight using SSL (same process as MySQL or Postgres)
    * Authentication using IAM token (same method as RDS)
    * protecting the instance with security groups 
    * you can't ssh
* Aurora Serverless
    * automated database installation and auto-scaling based on actual usage
    * good for infrequent, intermittent, unpredictable workloads
    * no capacity planning needed
    * pay per second, can be more cost-effective
* Global Aurora
    * Aurora Cross Region Read Replicas
        * useful for disaster recovery
        * simple to put in place
    * Aurora Global Database (recommended)
        * I Primary Region (read/write)
        * up to 5 secondary (read-ony) regions, replication lag is less than 1 second
        * up to 16 read replicas per secondary region
        * helps for decreasing latancy
        * promoting another region (for disaster recovary) has RTO of < 1 minute
        
### ElastiCache ###
* The same way RDS is to get managed Relational Databases
* ElasticCache is to get managed Redis or Memcached
* Caches are in-memory databases with really high performance, low latency
* helps reduce load off of databases for read intensive workloads
* helps make your application stateless
* write scaling using sharding (horizontal partition of data)
* read scaling using Read Replicas
* Multi AZ with Failover Capability
* AWS takes care of OS maintenace, patching, optimizations, setup, configuration, monitoring, failure recovery and backups

### ElastiCache Solution Architecture ###
* DB Cache
    * application queries ElastiCache, if not available, get from RDS and store in ElasticCache  
    * helps relieve load in RDS
    * cache must have an invalidation strategy to make sure only the most current data is used in there
* user session store
    * user logs into any of the application
    * the application writes the session data into ElastiCache
    * the user hits another instance of our application  
    * the instance retrieves the data and user is already logged in

### ElastiCache Redis vs Memcached ###
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
    
### ElastiCache Strategies  ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/15300184#content
* https://aws.amazon.com/caching/implementation-considerations    
* Not for every data,  data may be out of date, eventually consistent
* Caching types
    * Lazy Loading/ Cache-Aside / Lazy Population
 ![](.07_aws_RDS_Aurora_ElastiCache_images/aim3.jpg) 
        - pros
            * only requested data is cached (the cache isn't filled up with unused data)
            * node failures are not fatal (just increased latancy to warm the cache) 
        - cons
            * cache miss penalty that results in 3 round trips, noticeable delay for that request     
            * stale data: data can be updated in the database and outdated in the cache 
    * Write Though 
        * Add or Update cache when database is updated
         ![](.07_aws_RDS_Aurora_ElastiCache_images/aim4.jpg) 
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
         
### Create RDS ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851262#overview
1.Go to "RDS" service  
2.Create   
3.Select db - MySQL or PostgreSQL (free tier)  
    * fill the options   
    * name database - unique name in the region  
    * username/password  
    * select instance type
    
### Create Aurora ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19733954#overview

### Create ElastiCache ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851266#content