# Collections ###

### Hash and Equals Collections
* calculating hashCode number
* hashcode represents table index
* table buckets contains list of elements with the same hashcode
* to find element we will us equals method


### Abstract Classes and Interfaces ###
Abstract / Interface | Description | Implementation 
--- | --- | ---
*Iterable* |  iterating with a foreach statement | 
*Collection* |  common, generic interface functions
*List* |  for storing sequence of elements | Collection<E>, Iterable<E>
*Set, SortedSet, NavigableSet* | Dont allow duplicates
*Queue, Deque* | holds a sequence of elements for processing | LinkedList, ArrayDeque, LinkedBlockingDeque
*Map, SortedMap, NavigableMap* | maps key to values
*Iterator, ListIterator* | allows iterate over container

### Classes ###
Class | Description
--- | --- 
*ArrayList* |  Internally implemented as a resizable array. This is one of the most widely used concrete classes. Fast to search, but slow to insert or delete. Allows duplicates.
*DequeList* |  Internally implemented as a resizable array. Can add element only at the front or end of array.
*LinkedList* | Internally implements a doubly linked list data structure. Fast to insert or delete elements, but slow for searching elements. Additionally, LinkedList can be used when you need a stack (LIFO) or queue (FIFO) data structure. Allows duplicates.
*HashSet* | Internally implemented as a hash-table data structure. Used for storing a set of elements—it does not allow storing duplicate elements. Fast for searching and retrieving elements. It does not maintain any order for stored elements.
*TreeSet* | Internally implements a red-black tree data structure. Like HashSet, TreeSet does not allow storing duplicates. However, unlike HashSet, it stores the elements in a sorted order. It uses a tree data structure to decide where to store or search the elements, and the position is decided by the sorting order.
*HashMap* | Internally implemented as a hash-table data structure. Stores key and value pairs. Uses hashing for finding a place to search or store a pair. Searching or inserting is very fast. It does not store the elements in any order.
*TreeMap* | Internally implemented using a red-black tree data structure. Unlike HashMap, TreeMap stores the elements in a sorted order. It uses a tree data structure to decide where to store or search for keys, and the position is decided by the sorting order.
*PriorityQueue* | Internally implemented using heap data structure. A PriorityQueue is for retrieving elements based on priority. Irrespective of the order in which you insert, when you remove the elements, the highest priority element will be retrieved first.

### ArrayDeque ###
```java
import java.util.ArrayDeque;
import java.util.Deque;
class SplQueue {
    private Deque<String> splQ = new ArrayDeque<>();
    void addInQueue(String customer){
        splQ.addLast(customer);
    }
    void removeFront(){
        splQ.removeFirst();
    }
    void removeBack(){
        splQ.removeLast();
    }
    void printQueue(){
        System.out.println("Special queue contains: " + splQ);
    }
}
class SplQueueTest {
    public static void main(String []args) {
        SplQueue splQ = new SplQueue();
        splQ.addInQueue("Harrison");
        splQ.addInQueue("McCartney");
        splQ.addInQueue("Starr");
        splQ.addInQueue("Lennon");
        splQ.printQueue();
        splQ.removeFront();
        splQ.removeBack();
        splQ.printQueue();
    }
}
//Special queue contains: [Harrison, McCartney, Starr, Lennon]
//Special queue contains: [McCartney, Starr]
```