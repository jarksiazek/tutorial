### functions
* example 1
```kotlin
fun myFunction (param1: Int, param2: Int): Int {
    return param1 + param2
}

myFunction(10, 20)
```

* example 2
```kotlin
fun myFunction (param1: Int, param2: Int): Int = param1 + param2

myFunction(10, 20);
```

* example 3 with default value
```kotlin
fun myFunction (param1: Int = 1, param2: Int): Int = param1 + param2

myFunction(20);
```