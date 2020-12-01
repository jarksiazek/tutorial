### Lambda Limits ###
* per region
    * execution
        * memory allocation: RAM 128 - 3008 MB (64 increment)
        * maximum execution time: 900 seconds (15 mins)
        * environment variables: 4kb
        * disk capacity in the "function container" in /tmp: 512 MB
        * concurrency executions: 1000 (can be increased)
    * deployment
        * lambda function deployment size (compressed .zip): 50MB
        * uncompressed size (code+dependencies): 250MB
        * can use the /tmp directory to load other files at startup
        * environment variables: 4kb
