### CloudFormation ###
* declarative way of outlining your AWS Infrastructure, for any resources (most of them are supported)
* For Example:
    * I want to security group
    * I want to EC2 machines using this security group
    * I want two Elastic IPs for these EC2 machines
    * I want an S3 bucket
    * I want to ELB in front of these machines 

### Benefits of AWS CloudFormation ###
* Infrastructure as code
    * No resources are manually created 
    * the code can be version controlled for example using git
    * changes are reviewed through code
* cost
    * free
    * cost for stack (EC2, S3, etc..)
    * you can estimate the cost of your resources using the CloudFormation template
    * saving strategy: In dev you could automation deletion of template at 5PM and recreated at 8 AM, safely
* productivity
    * ability to destroy and re-create an infrastructure on the cloud on the fly
    * automated generation of Diagram for your templates
    * declarative programming (no need to figure out ordering and orchestration)
* separation of concern: create many stacks for many apps and layers
    * For example: 
        * VPC stacks
        * Network stacks
        * App stacks
* do not re-invent the wheel 
    * leverage existing templates on the web
    * leverage the documentation                       
    
### AWS CloudFormation - How works? ###
* templates on S3
* to update a template, we can't edit previous ones. We have to re-upload a new version of the template to AWS
* stacks are identified by a name
* deleting a stack deletes every single artifact that was created by CloudFormation

### Deploying CloudFormation ###
* manual way
    * editing templates in the CloudFormation Designer
    * using the console to input parameters, etc
* automated way
    * editing YAML file
    * using the AWS CLI to deploy the templates

### Building Blocks CloudFormation ###
* template components
    * resources declared in the template (MANDATORY)
    * parameters: the dynamic inputs for your template
    * mapping: the static variables for your template
    * conditionals: list of conditions to perform resource creation
    * metadata
* templates helpers
    * references
    * functions
    
### CloudFormation - Resources ###
* core of CloudFormation - MANDATORY
* represents the different AWS Components that will be created and configured
* resources are declared and can reference each other
* over 224 types of resources
* https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html
* resource types: identifiers are of them form: 
    * AWS::aws-product-name::data-type-name
* Example
    ```yaml
    Resource: 
        MyInstance:
            Type: AWS::EC2::Instance
            Properties: 
                AvailabilityZone: us-east-a1
                ImageId: ami-a4c7edb2
                InstanceType: t2.micro
                SecurityGroups:   
                    - !Ref SSHSecurityGroup  
                    - !Ref ServerSecurityGroup
    ```

                           
### CloudFormation - Parameters ###
* a way to provide inputs yo your AWS CloudFormation template
* important to know about if:
    * you want to reuse your templates across the company
    * some inputs cannot be determined ahead of time      
* parameters are extremely powerful, controlled and can prevent errors from happening in your templates thanks of types
* parameters settings
    * Type
        * String
        * Number
        * CommaDelimitedList
        * List<Type>
        * AWS Parameter (to help catch invalid values - match against existing values in the AWS Account)
    * Description
    * Constraints
    * ConstraintDescription
    * Min/MaxLength
    * Min/MaxValue
    * Defaults
    * AllowedValues(array)
    * AllowedPattern(regexp)
    * NoEcho(Boolean) 
* Example - refers to MyVPC Properties
    ```yaml
    Parameters:
        SecurityGroupDescription:
            Description: Security Group Description
            Type: String
            
    DbSubnet1:
        Type: AWS::EC2::Subnet
        Properties:
            VpcId: !Ref SecurityGroupDescription   
    ```

### CloudFormation - Mappings ###
* fixed variables within your CloudFormation Template
* they are very handy to differentiate between different environments (dev vs prod), regions (AWS regions), AMI types, etc
* all the values are hardcoded within the template
* Example1 
    ```yaml
    Mappings: 
      Mappings01: 
        Key01: 
          Name: Value01
        Key02: 
          Name: Value02
        Key03: 
          Name: Value03
    ```            
* Example2 
    ```yaml
    RegionMap: 
      us-east-1:
        "32": "ami-6411e20d" 
        "64": "ami-7a11e213" 
      us-west-1:
        "32": "ami-c9c7978c" 
        "64": "ami-cfc7978a" 
    ```   
* mappings vs parameters
    * mappings in advance all the values that can be taken and that can be deduced from variables such as: 
        * Region
        * AZ
        * AWS Account
        * Environment (dev vs prod)
    * they allow safer control over the template
    * use parameters when the values are really user specific
* Access Mapping Values
    * use Fn::FindInMap to return a named value from a specific key
    * !FindInMap [MapName, TopLevelKey, SecondLevelKey]
    * Example 
        ```yaml
        AWSTemplateFormatVersion: "2010-09-03"
        Mappings:
          RegionMap: 
            us-east-1:
              "32": "ami-6411e20d" 
              "64": "ami-7a11e213" 
            us-west-1:
              "32": "ami-c9c7978c" 
              "64": "ami-cfc7978a" 
        Resources:
          myEC2Instance:
            Type:"AWS::EC2::Instance"
            Properties:
              ImageId: !FindInMap [RegionMap, !Ref "AWS::Region", 32]
              InstanceType: m1.small
        ```           
 
 ### CloudFormation - Outputs ###
* declares optional outputs values that can import into other stacks (if you export them first)!           
* you can also view the outputs in the AWS Console or in using the AWS CLI
* they are very useful for example if you define a network CloudFormation and out the variables such as VPC ID and your Subnet IDs
* it is the best way to perform some collaboration cross stack, as you let export handle their own park of the stack
* you cannot delete a CloudFormation Stack if its outputs are being referenced by another CloudFormation stack
* Example
     ```yaml
      Outputs:
        StackSSHSecurityGroup: 
          Description: The SSH Security Group for our Company
          Value: !Ref MyCompanyWideSSHSecurityGroup
          Export:
            Name: StackSSHSecurityGroup 
    ```  
* Example - leverages above security group
     ```yaml
      Resources:
        MySecurityInstance: 
          Type: AWS::EC2::Instance
          Properties: 
            AvaiabilityZone: us-east-1a
            ImageId: ami-a4c7edb2
            InstanceType: t2.micro
            SecurityGroups:
              - !ImportValue StackSSHSecurityGroup
    ```       
 ### CloudFormation - Conditions ###
 * used to control the creation of resources or output based on condition
