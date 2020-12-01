### API Gateway - usage plans and API keys ###
* if you want ot make an API available as an offering ($) to your customers
* usage plan
    * who can access one or more deployed API stages and methods
    * how much and how fast they can access them 
    * uses API keys to identify API clients and meter access
    * configure throttling limits and quota limits that are enforced on individual client
* api keys
    * alphanumeric string values to distribute to your customer
    * can be used with usage plans to control access
    * throttling limits are applied to the API keys
    * quotas limits is the overall number of maximum limits

### API Gateway - correct order for API keys ###
* to configure a usage plan     
    1. create one or more APIs, configure the methods to require an API key, and deploy the APIs to stages
    2. generate or import API keys to distribute to application developers (your customers) who will be using your API
    3. create the usage plan with desired throttle and quota limits 
    4. associate API stages and API keys with the usage plan
* callers of the API must supply an assigned API key in the x-api-key header in requests to the API
