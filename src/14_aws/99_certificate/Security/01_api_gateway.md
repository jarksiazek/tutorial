### Q1
You have create REST API using API Gateway. Which of following mechanism can be used to deny specific IP address from accessing API Gateway
* AWS KMS 
* AWS Security Center
* **Resource Policy**
    * Resource Policies for API Gateway allows to deny or permit a specif IP address from where API Gateway can be accessed
* **AWS WAF**
    * AWS WAF (Web Application Firewall) - for Amazon API Gateway to protect attacks such as SQL injection and Cross-Site-Scripting (XSS). 
    * Additionally, you can filter web requests based on IP address, geographic area, request size, and/or string or regular expression pattern using the rules
    * https://aws.amazon.com/about-aws/whats-new/2018/10/amazon-api-gateway-adds-support-for-aws-waf/
    