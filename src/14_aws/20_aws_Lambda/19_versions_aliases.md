### Lambda Versions ###
* $LATEST - default version
* version - when publish new code then version will be changed
* version get their own ARN (Amazon Resource Name)
* Version = code + configuration
* each version of the lambda can be accessed

### Lambda Aliases ###
![](images/aim5.jpg)
* aliases are "pointer" to lambda function versions
* we can define a "dev", "test", "prod" aliases and have them point at the different lambda versions
* aliases are mutable
* aliases enable Blue/Green deployment by assigning weights to lambda functions
* aliases enable stable configuration of our event triggers/ destinations
* aliases have their own ARN's
* aliases cannot reference aliases

