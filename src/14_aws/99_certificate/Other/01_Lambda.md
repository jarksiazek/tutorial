### Q1
A developer has recently deployed an AWS Lambda function that computes a Fibonacci sequence using recursive Lambda invocations. A per-defined AWS IAM Policy is being used for this function, and only the required dependencies were packed. A few days after deployment, the Lambda function is being throttled.  
What should the Developer have done to prevent this, according to best practices? 
* Use more restrictive IAM policies
* **Avoid the use of recursion**
    * recursive call if the function within itself is not a recommended as a best practice 
    * https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html
* Request a concurrency service limit increase
* Increase the memory allocation range 

### Q2
A company is writing a Lambda function that will run in multiple stage, such a dev, test and production. The function is dependent upon several external services, and it must call different endpoints for these services based on functions deployment stage.   
What Lambda feature will enable the developer to ensure that code references the correct endpoints when running each stage? 
* Tagging
* Concurrency
* Aliases
* **Environment variables**
    * you can create different environment variables in the Lambda function that can be used to point to the different service. 
    * https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html