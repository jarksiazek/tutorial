### Slice 
* slice tricks - https://github.com/golang/go/wiki/SliceTricks


### Map
* ```var myMap1 map[string]int``` - string(key) - int(value)
* ```myMap2 := make(map[string]int, 1)``` - string(key) - int(value) size 1 
* ```myMap3 := map[string]int{"Mark": 1, "Maria": 2}```


* React if key not exist
  ```go
  if _, ok := myMap["Maria"]; !ok {
    fmt.Println("Key not found")
  }
  ```
  
* Find if key exists
  ```go
  if val, ok := myMap["Maria"]; ok {
    fmt.Println("Key found: ", val)
  }
  ```
 
* Loop map
  ```go
    for key, val :=range myMap {
      fmt.Println("key " + key +", value " + val)
    }
  ```
  
