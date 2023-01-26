### RDS Proxy
* connection between RDS and Lambda
* Lambda -> (IAM) -> VPC -> RDS Proxy -> RDS
* manages connection pools 
* can be located in public or private subnet

### Parameter group
* known for exam - rds.force_ssl=1
* changing pg required the db restart
