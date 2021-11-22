### Overview ###
* we want to give our users an identity so that they can interact with our application
* **Cognito User Pools**   
    * Sign in functionality for app users
    * Integrate with API Gateway and Application Load Balancer 
* **Cognito Identity Pools (Federated Identity)**   
    * provide AWS credentials to users, so they can access aws resources directly 
    * integrate with Cognito User Pools as an identity provider
* **Cognito Sync**
    * synchronize data from device to Cognito
    * is deprecated and replaced with AppSync

### Cognito vs IAM ###
* "hundreds of users"
* "mobile users"
* "authenticate with SAML"