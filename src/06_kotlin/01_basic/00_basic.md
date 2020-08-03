### Basic ###
https://try.kotlinlang.org

### Hello world

```kotlin
fun main (args: Array<String>) {
    println("Hello world")
}
```

### Variables
val -  value, used when the variable does not change (const)
var -  variable, can change over a program's lifetime
```kotlin
fun main (args: Array<String>) {
    val string = "Hello world" 
    var aString: String
    var aDouble: Double    
    
    println(string)
}
```
### Convert int to long
```kotlin
fun main (args: Array<String>) {
    val anInt: Int = 1
    val aLong: Long = anInt.toLong()
}
```

### if expression
```kotlin
fun main (args: Array<String>) {
   val lowest = if( a < b ) a else b;       
   println ("The lowest value is $lowest") 

   val lowest = if( a < b ) {
     println(a)
     a; 
   } else {
     println(b)
     b;
   };       
}
```

### switch expression
```kotlin
fun main (args: Array<String>) {
   val burgersOrdered = 2
    
    when(burgersOrdered) {
        0 -> println("Ordered 1")   
        1, 2 -> println("Ordered more than 2")   
        in 3..5 -> println("Ordered more than 3")   
        else -> {
            println("Ordered more than 5")
        }   
    }   
}
```