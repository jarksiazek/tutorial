* ```{} | jq '.'``` - unchanged output
* ```{} | jq '.[0]'``` - first element from array
* ```{} | jq '.[0] | {message: .commit.message}'``` - first element and only one field ```message```
* ```{} | jq '[.[] | {message: .commit.message}]'``` - from whole array take only the message
* 