### API Gateway - Security
* IAM Permission
    * create IAM Policy authorization and attach to User/Role
    * **Authentication = IAM and Authorization = IAM Policy**
    * Good to provide access within AWS (EC2, Lambda, IAM users...)
    * Leverage "Sig v4" capability where IAM credential are in headers
    ![](images/aim7.jpg)
* resource policy
    * similar to Lambda Resource Policy
    * allow for Cross Account Access (combined with IAM Security)
    * allow for specific source IP address
    * allow only for VPC endpoint
    
### API Gateway - Cognito
* Cognito - database for users
* Cognito - fully manages user lifecycle, token expires automatically
* API Gateway verifies  identity automatically from AWS Cognito
* No custom implementation required
* **Authentication = Cognito User Pools and Authorization = API Gateway Methods**
![](images/aim8.jpg)

### API Gateway - Lambda Authorizer (Custom Authorizer)
* token based authorizer (bearer token) - ex JWT (Json Web Token) or Oauth
* a request parameter-based lambda authorizer (header, query string, stage var)
* lambda must return an IAM policy for the user, result policy is cached 
* **Authentication = External and Authorization = Lambda function**
![](images/aim9.jpg)

### API Gateway - Summary
* IAM
    * Great for users/ roles within account AWS + resource policy for across account
    * handling authorization and authentication
    * leverage Sig 4
* Custom Authorizer
    * Great for 3rd part token
    * very flexible in terms of what IAM policy is returned
    * handle authorization and authentication in lambda function
    * pay for lambda invocations, results is cached
* Cognito
    * managing your own user pool (can be backed by FB,Google login etc)
    * no need extra code
    * must implement authorization in the backend
    






 
 