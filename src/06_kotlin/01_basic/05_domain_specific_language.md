### DSL - domain specific language
```kotlin
interface Matcher<T> {
    fun test(lhs: T): Unit
    
    infix fun or(other: Matcher<T>): Matcher<T> = object: Matcher<T> {
        overrride fun test(lhs: T) {
            try {
                this@Matcher.test(lhs)
            } catch (e: RuntimeException) {
                other.test(lhs)
            }       
        }   
    }
}

infix fun <T>T.should(matcher: Matcher<T>) {
    matcher.test(this)
}    
```
