### Elastic Beanstalk Deployment Process ###
* describe dependencies (requirements.txt for Python, package.json for Node.js)
* package code as zip and describe dependencies
    * Python: requirements.txt
    * Node.js package.json
* Console: upload zip file (create new app version), and then deploy
* Beanstalk will deploy the zip on each EC2 instance, resolve dependencies and start the application