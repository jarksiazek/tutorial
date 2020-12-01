### Cognito Identity Pool - Federated Identities ###
![](images/aim3.jpg)
* get identities for "users" so they obtain temporary AWS credentials
* your identity pool (eg. identity source) can include
    * public providers (Login with Amazon, FB, Google, Apple)
    * users in an Amazon Cognito user pool
    * OpenID Connect Providers and SAML Identity Providers
    * Developer Authenticated Identities (custom login server)
    * Cognito Identity Pools allow for unauthenticated (guest) access
* users can then access AWS services directly or through API Gateway
    * the IAM policies applied to the credentials are defined in Cognito
    * they can be customized based on the user_id for fine gained control  

### Cognito Identity Pool - IAM Roles ###
* default IAM roles for authenticated and guest users
* define rules to choose the role for each  user based on the user's ID
* can partition your users' access using policy variables
* IAM credentials are obtained by Cognito Identity Pools through STS 
* the roles must have a "trust" policy  of Cognito Identity Pools
