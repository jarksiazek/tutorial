### Q1
a developer is migrating an on-premise application to AWS. The app currenctly uses Microsoft SQL, encrypting some of the data using Transparent Data Encryption.   
Which service should the developer use to minimize code changes? 
* **RDS**
    * RDS supports Transparent Data Encryption (TDE) o encrypt data on DB instances running Microsoft SQL Server. TDE automatically encrypts data before it is written to storage and automatically decrypts data when the data is read from storage
* Aurora
* Redshift
* DynamoDB

### Q2
You are using DynamoDB as a database to save sales data for global appliance company. All data at rest is encrypted using KWS.  
Which of the following can be used for encryption of global secondary index with min cost? 
* Data Keys with AWS Managed CMK
* Table Keys with AWS Managed CMK
* **Data Keys with AWS owned CMK**
    * DynamoDB uses the CMK to generate and encrypt a unique data key fo the table, know as the table key. With DynamoDB, AWS Owned, or AWS Managed CMK can be used to generate and encrypt keys. 
    AWS Owned CMK is free of charge while AWS Managed CMK is chargeable. Customer managed CMK's are not supported with encryption at rest.
    ""With encryption at resty, DynamoDB transparently encrypts all customer data in a DynamoDB table, including its primary key and local and global secondary indexes, whenever the table is persisted to disk 
    * https://docs.aws.amazon.com/kms/latest/developerguide/services-dynamodb.html
* Table Keys with AWS owned CMK

### Q3
Yor company is going to develop and application with DynamoDB. There is a requirement that all data needs to be encrypted at rest.  
If the dynamoDB has already been created, what else is needed to achieve this? 
* **No additional configuration are required since server-side encryption is enabled on all DynamodDB table data.** 
* Enable encryption on the existing table
    * encryption can only be configurated during table creating time
* You cannot enable encryption at rest. Consider using the AWS RDS service instead. 
* You cannot enable encryption at rest. Consider using the S3 service instead. 