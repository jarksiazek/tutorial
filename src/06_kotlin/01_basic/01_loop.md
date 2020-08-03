### loops
* example 1
```kotlin
fun main (args: Array<String>) {
    
    for (item in 1..10) {
        println("$item")
    }
}
```
* example 2
```kotlin
fun main (args: Array<String>) {
    
    for (item in 10.rangeTo(20).step(1)) {
        println("$item")
    }
}
```

* example 3 with index
```kotlin
fun main (args: Array<String>) {
    
    for ((index, item) in 10.rangeTo(20).step(1).withIndex()) {
        println("$item, index: ${index + 1} ")
    }
}
```

* example 4 for array
```kotlin
fun main (args: Array<String>) {
    
    val myArray = arrayOf(10, 20, 30, 40)
    for (item in myArray.indeces) {
        println("Index: $item") //item is index not the value
        println("Value: ${myArrays[item]}") 
    }
}