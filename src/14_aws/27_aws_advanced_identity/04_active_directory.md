### Microsoft Active Directory
* found on any Windows Server and AD Domain Services
* database of objects: User Accounts m Computers, Printers, File Shares, Security Groups 
* centralized security management, create account, assign permissions 
* objects are organized in tree
* a group of trees is a forest

### AWS Directory Services
* AWS Managed Microsoft AD 
    * create your onw AD in AWS, manage users locally, supports MFA
    * establish "trust" connections with your on-premise AD
    ![](images/aim7.jpg)

* AD Connector
    * Directory Gateway (proxy) to redirect to on-premise AD
    * users are managed the on-premise AD 
    ![](images/aim8.jpg)

* Simple AD
    * AD-compatible managed directory on AWS
    * cannot be joined with on-premise AD
    
