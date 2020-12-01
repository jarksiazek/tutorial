### CloudWatch Logs - encryption ###
* can encrypt logs with KMS
* enable at log group level, by associating a CMK with a log group, either when you create the log group or after is exists
* you cannot associate a CMK with a log group using the CloudWatch console
* you must use the CloudWatch Logs API
    * associate-kms-key: if the log group already exists
    * create-log-group: if the log group does not exist yet

