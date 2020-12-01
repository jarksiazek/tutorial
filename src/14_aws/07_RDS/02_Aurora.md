### Aurora ###
* is not open source (AWS product)
* Postgres and MySQL are both supported as Aurora DB(your drivers will work as if Aurora was a Postgres or MySQL database)
* cloud optimized, claims 5x performance improvement over MySQL, 3x over Postgres
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
![](images/aim2.jpg) 
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
        * helps for decreasing latency
        * promoting another region (for disaster recovery) has RTO of < 1 minute