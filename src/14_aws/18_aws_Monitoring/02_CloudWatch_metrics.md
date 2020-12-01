### AWS CloudWatch Metrics
* CloudWatch provides metrics for every services in AWS 
* metric is variable to monitor (CPU Utilization, NetworkIn ...)
* metrics belong to namespaces 
* dimension is an attribute of a metric (instance id, environment, etc)
* up to 10 dimensions per metric 
* metrics have timestamps
* can create dashboards of metrics 

### AWS CloudWatch EC2 Detailed monitoring
* EC2 have metrics every 5 mins 
* with detailed monitoring (for a cost) you can get every 1 min metrics
* use detailed monitoring if you want to more prompt scale your ASG
* Free Tier allows us to have 10 detailed monitoring metrics
* EC2 memory usage is by default not pushed (must be pushed from inside the instance as custom metric)
* Custom metrics 
    * possible to define and send custom metrics to CloudWatch
    * ability to use dimension (attributes) to segment metrics
        * instance.id
        * environment.name
    * metric resolution
        * standard is one minute
        * high resolution up to one sec - high cost
    * use API call PutMetricData
    * exponential backup - when pushing too many data