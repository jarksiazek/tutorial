### DynamoDB Security
* security
    * VPC Endpoints available to access DynamoDB without internet
    * access fully controlled by IAM
    * encrypting at rest using KMS
    * encrypting in transit using SSL/TLS
* backup and restore a feature available  
    * point in time restore like RDS 
    * no performance impact
* global tables
    * multi region, fully replicated, high performance
* Amazon DMS can be used to migrate to DynamoDB (from Mongo, Oracle, MySQL, S3, etc...)
* you can launch a local DynamoDB on your computer for development purpose
