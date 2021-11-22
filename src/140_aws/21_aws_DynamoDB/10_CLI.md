### DynamoDB CLI
* --projection-expression: attributes to retrieve
* --filter-expression: filter results
* general CLI pagination options including DynamoDB/S3
    * optimization
        * --page-size: full dataset is still received but each API call will request less data
    * pagination
        * --max-items: max number of results returned by the CLI. Retruns *NextToken*
        * --starting-token: specify the last received *NextToken* to keep on reading


