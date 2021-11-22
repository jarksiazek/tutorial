### Lambda dependencies ###
* if Lambda function depends of external libraries
* you need to install the packages alongside your code and zip it together
* upload the zip straight yo Lambda if less than 50 MB else to S3  
* native libraries work: they need to be complied on Amazon Linux
* AWS SDK comes by default with every Lambda function