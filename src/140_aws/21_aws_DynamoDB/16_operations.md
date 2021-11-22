### DynamoDB Operations
*  Table cleanup:
    * option 1: Scan + Delete => very slow, expensive, consumes RCU/WCU
    * option 2: Drop table + recreate a table => fast, cheap, efficient
*  Copy Table:
    * option 1: use AWS DataPipeline (use EMR)
    ![](images/aim13.jpg)
    * option 2: create a backup and restore the backup in to a new name (can take some time)
    * option 3: Scan + write => write own code
    
