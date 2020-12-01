### Deployment Stages ###
* making changes in the API Gateway does not mean they're effective
* you need to make a "deployment" for them to be in effect
* it's a common source of confusion
* changes are deployed to stages (many as you want)
* each stage has its own configuration parameters
* stages can be rolled back as a history of deployments is kept

### Stage Variables ###
* stage variables are like environment variables for API Gateway
* use them to change often changing configuration
* they can be used in:
    * Lambda function ARN
    * HTTP Endpoint
    * Parameter mapping templates
* use cases: 
    * configure HTTP endpoints your stages talk to (dev,test,prod)
    * pass configuration parameters to AWS Lambda through mapping templates
* stage variables are passed to context object in AWS Lambda

