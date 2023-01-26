### type MyFunc = func(x, y int) int 
```go
type MyFunc = func(x, y int) int 

func main (){
  var f MyFunc = func(a, b int) int {
    return a + b
  }
  
  x:=f(1,5)
}
```

### MyFunc := func(num ..int) {}
```go
func main (){
  MyFunc := func(num ..int) {
    fmt.Println(num)
  }
  
  MyFunc(1)
  MyFunc(1,3)
}
```

### autoexecution
```go

txt:="Text for function"

func(t string) {
  fmt.Println(t)
}(txt)
```

### pointer receivers 
https://go.dev/tour/methods/4
```go
type Vertex struct {
  X, Y float64
}
func (v Vertex) Abs() float64 {
  return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
func main() {
  v := Vertex{3, 4}
  v.Scale(10)
  fmt.Println(v.Abs())
}
```

