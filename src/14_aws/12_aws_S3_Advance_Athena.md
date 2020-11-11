### S3 MFA Delete ###
* https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729198#content
* MFA multi factor authentication - (additinal code on device) before doing important operations on S3
* To use MFA-delete, enable Versioning on S3 bucket
* needs MFA to
    * permanently delete an object version
    * suspend versioning on the bucket 
* don't need MFA
    * enabling versioning
    * listing deleted versions
* only the bucket owner (root account) can enable/disable MFA-Delete
* MFA-delete currently can only be enabled using CLI - no console

### S3 Access Logs ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729204#content
* for audit purpose, you may want to log all access to S3 buckets
* any request made to S3, from any account, authorized or denied, will be logged into another S3 bucket
* data can be analyzed using data analysis tools or Amazon Athena
* Warning:
    * keep logs in separate buckets for logs and monitored bucket
        
        
### S3 Replication CRR & SRR ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729208#content
* CRR - cross region replication
* SRR - same region replication
* Must enable versioning in source and destination
* Buckets can be in different accounts
* Copying is asynchronous, but is quick
* Must give proper IAM permission to S3
* CRR - Use cases: compliance, lower latency access, replication across account  
* SRR - Use cases: log aggregation, live replication between production and test accounts  
* Notes
    * only new objects are replicated (not retroactive)
    * for delete operations
        * if you delete without a version ID, it adds a delete marker, not replicated
        * if you delete with a version ID, it deletes in the source, not replicated
        
    * no "chaining" of replication 
        * if bucket 1 has replication into bucket 2, which has replication into bucket 3 
        * then objects created in bucket 1 are not replicated to bucket 3
        
### S3 pre-signed URLs ###
* https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729210#content
* Can generate pre-signed URLs using SDK or CLI
    * for downloads (easy, can use the CLI)
    * for uploads (harder, must use the SDK)
* Valid for default of 3600 seconds, can change timeout with --expires-in [TIME_BY_SECONDS] argument
* Users given a pre-signed URL inherit the permissions of the person who generated the URL for GET/PUT
* Examples:
    * Allow only logged-in users to download a premium video on your S3 bucket
    * Allow an ever changing list of users to download files by generating URLs dynamically
    * Allow temporarily a user to upload a file to a precise location in our bucket
    
### S3 Storage Tiers ###
* https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729212#content
* S3 Storage Classes
    * Amazon S3 Standard - General Purpose
        * high durability 99.999999% of objects across multiple AZ
        * 99.99% availability over a given year
        * sustain 2 concurrent facility failures
        * Use case:
            big data, mobile & gaming applications, content distribution  
    * Amazon S3 Standard - Infrequent Access (IA)
        * data with less frequently access, but rapid when needed
        * high durability 99.999999% of objects across multiple AZ
        * 99.9% availability over a given year
        * lower than S3 Standard
        * sustain 2 concurrent facility failures
        * Use case:
            data store for disaster recovery, backups
    * Amazon S3 One Zone - Infrequent Access
        * same as IA, data store in one AZ
        * high durability 99.999999% of objects in single AZ, data lost when AZ is destroyed
        * 99.5% availability over a given year
        * supports SSL for data at transit an encryption at rest 
        * low cost than IA (20%)
        * Use case:
            storing secondary backup copiers of on-premise data, storing data you can recreate     
    * Amazon S3 Intelligent Tiering
        * same low latency, durability and high throughput performance of S3 Standard
        * small monthly monitoring and auto-tiering fee
        * automatically moves objects between two access tiers based on changing access patterns
        * resilient against events that impact an entire AZ
        * 99.9% availability over a given year
    * Amazon Glacier
        * low cost object storage meant for archiving /backup
        * data is retained for longer term (10 years)
        * alternative to on-premise magnetic tape storage
        * same durability as S3 standard
        * cost per storage per month ($0.004/GB) + retrieval cost
        * each item in Glacier is called "Archive" (up to 40 TB)
        * archives are stored in "Vaults"
   * Amazon Glacier
        * 3 retrieval options
            * expedited (1 to 5 minutes)
            * standard (3 to 5 hours)
            * bulk (5 to 12 hours)                 
            * minimum storage duration of 90 days
    * Amazon Glacier Deep Archive
        * for long term - cheaper
        * retrieval options
            * standard 12 hrs
            * bulk 48 hrs
            * min storage is 180 days
    * Amazon S3 Reduced Redundancy Storage (deprecated - omitted)

### S3 Moving between storage classes ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729220#content
    ![](.12_aws_S3_advance_images/aim1.jpg)
* you can transition objects between storage  classes
* IA -> Standard 
* Glavier -> Glacier Deep Archive
* Moving can be automated usign a lifecycle configuration
* S3 Lifecycles Rules
    * transition actions: it defines when objects are transitioned to another storage class
        * move objects to Standard IA class 60 days after creation
        * move to glacier for archiving after 6 months
    * expiration actions: configue objects to expire (delete) after a mount of time
        * access log files can be set to delete after 365 days
        * delete an old version of the file (if versioning is enabled)
        * delete incomplete multi-part uploads
    * rules can be created for specific prefix (ex. s3://mybucket/mp3/*)
    * rules can be created for specific tags
               
### S3 Performance ###
* automatically scales to high request rates, latency 100-200ms
* 3500 PUT/COPY/POST/DELETE per sec per prefix in bucket
* 5500 GET/HEAD per sec per prefix in bucket
* No limits to the number of prefix
    * Example (object path => prefix)
        * bucket/folder1/sub1/file => /folder1/sub1/
        * bucket/folder1/sub2/file => /folder1/sub2/
        * bucket/2/file => /2/
* KMS Limitation for S3 performance
    * when you use SEE-KMS, you may be impacted by the KMS limits
    * when you upload, it calls the GenerateDataKey KMS API
    * when you download, it calls the Decrypt KSM API
    * count towards the KMS quota per second 
        (depends on region 5500, 10000 or 30000 req/s)
* Performance optimization
    * multi-part upload
        ![](.12_aws_S3_advance_images/aim2.jpg)
        * recommended for files > 100 MB
            must use for files > 5 GB
        * parallelize uploads   
    * S3 Transfer Acceleration(only upload)
          ![](.12_aws_S3_advance_images/aim3.jpg)
        * increase transferring file to an AWS edge location which will forward the data to the S3 bucket in the target region
        * compatible with multi-part upload
    * S3 Byte-Range Fetches
        * parallelize GETs by requesting specific byte ranges
        * better resilience in case of failures
        * divides file into many small files and download them parallelly
        * divides file into many small files and first fetch only first on which contains header   
        
### S3 Event Notification ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19735990#content
* ObjectCreated, ObjectRemoved, etc
* reacts on s3 data events
* object name filtering possible (*.jpg)
* use case: generate thumbnails of images uploaded to S3
* types
    * SNS Topic 
    * SQS Queue
    * Lambda Function
    
### S3 Object Lock & Glacier Vault Lock ###
* S3 Object Lock
    * Adopt a WORM (Write Once Read Many)
    * Block an object version deletion for a specific amount of time
* Glacier Vault Lock
    * Adopt a WORM (Write Once Read Many)
    * Lock the policy for future edits (can no longer be changed) 
    * helpful  for compliance and data retention 
    
### AWS Athena ###
* Serverless service to perform analytics directly against S3 files
* SQL language to query the files
* has JDBC / ODBC driver
* charged per query and amount of data scanned
* Supports CSV, JSON, ORC, Avro and Parquet (built on Presto - query engine)
* Use cases 
    * BI, analytics, reporting and query VPC Flow Logs, ELB Logs, CloudTrail, etc
     