### Elastic Beanstalk Extensions ###
* a zip file containing our code must be deployed to Elastic Beanstalk
* all the parameters set in the UI can be configured with code using files
* Requirements 
    * in the **.ebextensions/** directory in the root of source code
    * YAML/JSON format
    * .config extensions(example: logging.config)
    * able to modify some default setting using: option_settings
    * ability to add resources such as RDS, ElasticCache, DynamoDB, etc
* Resources maanged by .bextensions get deleted if the environment goes away     