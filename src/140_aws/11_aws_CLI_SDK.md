### AWS CLI INSTALLATION ###
* Installing CLI on windows
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851272#overview
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html
```bash
//veriify if the cli is installed
$ aws --version
```

### AWS CLI CONFIGURATION ###
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851278#overview
1. IAM -> Users -> Security credentials -> "Create access key"
2. Back to CLI
    * go to configuration
    ```bash
    $ aws configure
    ```
   * Put access Key and secret access key

### AWS CLI S3 ###
* aws doc - https://docs.aws.amazon.com/cli/latest/reference/s3/
https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851280#overview

### TESTING POLICY ###
* aws policy simulator
    * https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html
* cli dry run
    * use "--dry-run"    
    
### STS ###
* CLI STS decode errors
    * https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851308#overview
    * https://docs.aws.amazon.com/cli/latest/reference/sts/decode-authorization-message.html 
    * error message which is shown during cli operations
    * sts decode-authorization-message
    * example
    ```bash
    //before run, make sure that you have proper STS policy permission
    $ aws sts decode-authorization-message --encoded-message khj23jk1gh231    
    ```

### EC2 Instance Metadata ###
* https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851286#overview
* it allows AWS EC2 instances to "learn about themselves" without using an IAM Role for that purpose
* The URL is http://169.254.169.254/latest/meta-data
* you can retrieve the IAM Role name from the metadata, but you CANNOT retrieve the IAM Policy
* Metadata = Info about the EC2 instance
* Userdata = launch script of the EC2 instance

### MFA with CLI ###
* MFA - multi factor authentication
* to use it with CLI, you must create a temporary session
* to do that, you must run STS GetSessionToken API
* example   
    *
    ```bash
    $ aws sts get-session-token --serial-number arn-of-the-mfa-device-code code-from-token --duration-seconds 3600 
    ```

### AWS SDK ###
* use action directly from the code
* default region is us-east-1

### AWS Limits (Quotas) ###
* API Rate Limits
    * ex. DescribeInstances API for EC2 has limit of 100 calls per second
    * ex. GetObject on S3 has limit of 5500 GET per second per prefix
      
* Service Quotas (Service Limits)
    * Running On-demand Standard Instances: 1152 vCPU's
    * to increase limits you need to open a ticket
    * or use quota using the Service Quotas API
    
### AWS CLI Credentials Provide Chain ###
* CLI looks for credentials in this order
    * command options --region, --output, --profile
    * environment variables AWS_ACCESS_KEY_ID, SECRET_KEY, AWS_SESSION_TOKEN
    * CLI credentials file -- aws comfigure
    * CLI configuration file -- aws comfigure
    * ECS Container credentials
    * Instance profile credentials
* SDK defaul order 
    * environment variables AWS_ACCESS_KEY_ID, SECRET_KEY
    * java system properties
    * default credential profiles file
    * ECS Container credentials
    * Instance profile credentials

### Signing AWS API requests ###
* HTTP request must be signed by AWS credentials(access key & secret key)
* some request to S3 don't need to be signed
* If you use the SDK or CLI, the Http requests are signed for you
* you should sign an AWS HTTP request using Signature v4 (Sigv4)
