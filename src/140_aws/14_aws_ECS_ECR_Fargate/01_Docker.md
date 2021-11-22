### DOCKER ###
* is a software development platform to deploy apps
* apps are packaged in containers that can be run on any OS
* apps run the same, regardless of where they're run
    * any machine
    * no compatibility issue
    * predictable behaviour
    * less work
    * easier to maintain and deploy
    * run docker container on EC2
* storing docker images
    * public:dockerhub
    * private: Amazon ECR (Elastic Container Registry)
* docker containers management 
    * container management platform
        * ECS: Amazon's own platform
        * Fargate: Amazon's own Serverless platform
        * EKS: Amazon;s managed Kuberneter (open source)
        
### DOCKER VS VIRTUAL MACHINE ###
![](images/aim1.jpg)
* docker is "sorf of" a virtualization technology, but not exactly
* resources are shared with the host => many container on one server
* lighter than vm 