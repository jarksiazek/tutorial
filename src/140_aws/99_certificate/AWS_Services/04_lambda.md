### Q1
You'are developing an application onto AWS which is based on the Microservices. These Microservices will be created on AWS Lambdas. 
Because of the complexity of the flow of these different components, you need some way to manage the workflow of execution of these various Lambdas.  
How could you manage this effectively now and for the future addition of Lambdas to the application? 
* Consider creating a master Lambda that would coordinate the execution of the Lambdas
* Consider creating a separate application hosted on an EC2 
* **Consider using Step Functions**
    * https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html
    * step functions provides a reliable way to coordinate components and step through the functions of your application
* Consider using SQS queues 

### Q2
Your AWS Lambda function writes to an S3 bucket. Which of the following is the best practice to pass operation parameters, such as the bucket name, to your Lambda function?
* **Configure S3 bucket name with AWS Lambda Environment Variables**
    * https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html
* Hard Code S3 bucket name to Lambda
* Configure S3 bucket name with AWS Lambda Function Variables
* Configure an Alias with S3 and pass it to Lambda Function

### Q3
You are using S3 buckets to store images. These S3 buckets invoke a lambda on upload. The lambda creates thumbnails of the images and stores them in other S3.  
An AWS CloudFormation template is used to create the Lambda function with resource "AWS::LambdaFunction".  
Which of the following functions would be call to execute this? 
* FunctionName
* Layers
* Environment
* **Handler**
    * the handler is the name of the method within a code that Lambda calls to execute the function.

### Q4
You are developing a function that will be hosted in AWS Lambda. The function will be developed in .Net. There a number of external libraries that are needed for the code.  
Which of the following is the best practice when it comes to working with external dependencies for AWS Lambda.
* Make sure that the dependencies are put in the root folder
* **Selectively only include the libraries that are required** 
    * minimize your deployment package size to its runtime necesseries. 
    * Avoid uploading the entire SDS library, selectively depend on the modules which pick up
    * https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html
* Make sure the libraries are installed in the beginning of the function 
* Place the entire SDK dependencies in S3 

