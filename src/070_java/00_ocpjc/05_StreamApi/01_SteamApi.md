# Stream #


### Search Data from a Stream
Method name |  Description
--- | --- 
boolean anyMatch(Predicate<? super T> check) | Returns true if there is any elements in the stream that matches the given predicate. Returns false if the stream is empty or if there are no matching elements. 
boolean allMatch(Predicate<? super T> check) | Returns true only if all elements in the stream matches the given predicate. Returns true if the stream is empty without evaluating the predicate! 
boolean noneMatch(Predicate<? super T> check) | Returns true only if none of the elements in the stream matches the given predicate. Returns true if the stream is empty without evaluating the predicate!
Optional<T> findFirst() | Returns the first element from the stream; if there is no element present in the stream, it returns an empty Optional<T> object.
Optional<T> findAny() | Faster than findFirst in parallel stream. Returns one of the elements from the stream; if there is no element present in the stream, it returns an empty Optional<T> object.

### Optional
Method | Example 
--- | ---
Optional<T> max(Comparator<? super T> comparator); | Steam.of(1.1, 1.2).max(Double::compareTo));
