### struct
```go
type Car struct {
  model string
  year int
}
```

### pointer
* https://github.com/golang/go/wiki/CodeReviewComments#receiver-type
* example 1 
  ```go
  a := 1000 //100
  pointer := &a //address in memory
  ``` 
* example 2
  ```go
  a := new(int) //address in memory
  val := *a //value from memory
  ``` 
