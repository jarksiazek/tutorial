# Stream and Filters 
* stream of object references (uses for Collection interface)
* IntStream, LongStream and DoubleStream are streams for primitive types
* use for List, Set, Deque, Queue (extends Collection)

### Stream Pipeline
* source: *of()*, *generate()*
* intermediate operations: *map()*, *filter()*, *distinct()*, *sorted()*
* terminal operations: *sum()*, *collect()*, *forEach()*, *reduce()*

### Intermediate operations
Method | Description
--- | --- 
Stream<T> filter(Predicate<? super T> check) | removes elements when check return *false*
<R> Stream<R> map(Function<? super T,? extends R> transform) | applies transform function
Stream<T> distinct() | Removes duplicate elements in the stream; it uses the *equals()*
Stream<T> sorted() | Sorts the elements in its natural order
Stream<T> sorted(Comparator<? super T> compare) | Sorts the elements using Comparator
Stream<T> peek(Consumer<? super T> consume) | Returns the same elements in the stream, but also executes the passed consume lambda expression on the elements.
Stream<T> limit(long size) | Removes the elements if there are more limit

### Terminal operations
Method | Description
--- | --- 
void forEach(Consumer<? super T> action) | Calls the action for every element in the stream.
Object[] toArray() | Returns an Object array that has the elements in the stream.
reduce() | 
findFirst(), findAny(), allMatch() | 
collect() | 

