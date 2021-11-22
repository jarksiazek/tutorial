### Lambda CloudFormation - inline ###
* use for very simple function, do not included dependencies

### Lambda CloudFormation - through S3 ###
* attaching zip with will all dependencies
* essential location information
    * S3Bucket
    * S3Key: full path to zip 
    * S3ObjectVersion: if versioned bucket
