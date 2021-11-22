### SSM Parameter Store vs Secrets Manager ###
* Secrets Manager ($$$)
    * automatic rotation of secrets with Lambda
    * direct integration with RDS, Redshift and DocumentDB
    * KMS is mandatory
    * can integrate  with CloudFormation
* SSM Parameter Store ($)
    * Simple API
    * no secret rotation
    * KMS encryption is option
    * can integrate  with CloudFormation
    * can pull a Secret Manager secret using the SSM Parameter Store API
    

