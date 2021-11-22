### Granting a User Permissions to Pass a Role to an AWS Service ###
* to configure many AWS services, you must pass an IAM role to the service (this happens only once during setup)
* the service will later assume the role and perform actions
* example of passing a role
    * to an EC2 instance
    * to a Lambda
* for this, you need the IAM permission **iam:PassRole**    
* it often comes with **iam:GetRole** to view the role being passed

### IAM PassRole example
![](images/aim5.jpg)
* can a role be passed to any service?
    * No: Roles can only be passed to what their **trust** allows 
    * a *trust policy* for the role that allows the service to assume the role
    ![](images/aim6.jpg)

         
     
    