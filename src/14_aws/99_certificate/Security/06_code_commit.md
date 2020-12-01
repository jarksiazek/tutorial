### Q1
Your team has a Code Commit repository in your account. You need to give developers in another account access yo your Code Commit repository.  
Which of the following is the most effective way to grant access? 
* Create IAM users for each developer and provide access to the repository
* Create an IAM Group, add the IAM users and then provide access to the repository
* **Create a cross account role, give the role privileges. Provide the role ARN to the developers.**
    * https://docs.aws.amazon.com/codecommit/latest/userguide/cross-account.html
* Enable public access to the repository.
 
   