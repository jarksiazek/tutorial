### Q1
you are using AWS SAM to define a Lambda and configure CodeDeploy to manage deployment patterns.  
With new Lambda function working as per expectation which of the following will shift traffic from an original Lambda to new in the shortest time frame?
* **Canary10Percent5Minutes**
    * 10 percent is shifted in the first interval while remaining all traffic is shifted after 5 minutes
* Linear10PercentEvery10Minutes
    * will add 10 percent linearly to new version every 10 minutes
* Canary10Percent15Minutes
* Linear10PercentEvery5Minutes

### Q2
Which of the following is the right sequence of hooks that get called in AWS CodeDeploy?
* **Application Stop->BeforeInstall->After Install->Application Start**
    * https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file-structure-hooks.html#reference-appspec-file-structure-hooks-run-order
    * ![](images/aim2.jpg)
* BeforeInstall->After Install->Application Stop->Application Start
* BeforeInstall->After Install->Validate Service->Application Start
* BeforeInstall->Application Stop->Validate Service->Application Start

