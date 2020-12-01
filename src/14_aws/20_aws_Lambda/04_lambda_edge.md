### Lambda@Edge
* you have deployed a CDN using CloudFront
* global using AWS Lambda
* implement filtering before reaching your application 
* Lambda@Edge: 
![](images/aim11.jpg)
    * deploying function alongside your CloudFront CDN
    * change CloudFront requests and responses
        * after CloudFront receives a request from viewer
        * before CloudFront forwards the request to the origin request
        * after CloudFront receives the response from the origin
        * before CloudFront forwards the reponse to the viewer 
    * use case
        * website security and Privacy
        * Dynamic Web Application at the Edge
        * SEO
        * Intelligently Route Across Origins and Data Center
        * Bot Mitigation at the Edge
        * Real time image transformation 
        * A/B Testing
        * User authentication and authorization
        * user prioritization
        * user tracking and analytics 
