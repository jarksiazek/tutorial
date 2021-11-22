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
        * continuous backups and restore a specific timestamp
        * monitoring dashboard to monitor db
        * read replicas for improved performance 
        * multi AZ setup for DR (Disaster Recovery)
        * maintenance windows for upgrades
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
* replicas can be promoted to their own DB
* applications must update the connection string to leverage read replicas
* read replicas are used for SELECT (=read) only kind of statements (not INSERT, UPDATE, DELETE)  
![](images/aim1.jpg) 
* Read Replicas - Network Cost
    * network cost when data goes from one AZ to another 
    * reduce cost keeping the Read Replicas in the same AZ - it's free

### RDS Multi AZ -DR (Disaster Recovery) ###
* SYNC replication
* failover in case of loss of AZ, loss of network, instance or storage failure
* The Read Replicas can be setup as Multi AZ for DR

### RDS Security - Encryption ###
* at rest encryption
    * possibility to encrypt the master & read replicas with AWS KMS - AES-256 encyption
    * encryption has to be defined at launch time
    * if the master is not encrypted, the read replicas cannot be encrypted
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
            * can leverage IAM Roles and EC2 Instance profiles for easy integration