### STS - Security Token Service ###
* allows for granting limited and temporary access to AWS resources (up to 1 hour)
* **AssumeRole** - assume roles within your account or cross account
* **AssumeRoleWithSAML** - return credentials for users logged with SAML
* **AssumeRoleWithWebIdentity** - 
    * return creds for users logged with and IdP (FB login, Google Login, OIDC compatible...)
    * AWS recommends against using this and using Cognito Identity Pools instead
* **GetSessionToken** for MFA, from a user or AWS account root user
* **GetFederationToken** obtain temporary creds for a federated user
* **GetCallerIdentity** return details about the IAM user or role used in the API call
* **DecodeAuthorizationMessage** decode error message when an AWS API is denied

### STS - Security Token Service ###
![](images/aim1.jpg)
* define an IAM Role within your account or cross-account
* define which principals can access this IAM Role
* use AWS STS to retrieve credentials and impersonate the IAM Role you have access to (AssumeRole API)
* temporary credentials can be valid between 15 mins to 1 hour

### STS - Cross account access with STS ###
![](images/aim2.jpg)

### STS - with MFA ###
![](images/aim3.jpg)
* use **GetSessionToken** from STS
* appropriate IAM policy using IAM Conditions
* **aws:MultiFactorAuthPresent:true**
* Reminder, GetSessionToken returns:
    * Access ID
    * Secret Key
    * Session Token
    * Expiration date
    * 
    