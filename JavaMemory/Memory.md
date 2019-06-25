##Memory


###Stack
- First in, last out
- Every thread has its own stack
- JVM know when to destroy stack(like after one function ends)

![stack](../image/stack.png)

###Heap
- all objects are stored on the heap
- object in heap that can shared across multiple threads
- variable are a reference to the objects
- local variables are stored on the stack

![stack](../image/heap.png)

###Pass by value
- For Primitives, pass by value
- For objects, the Reference to the object is passed by value(we are passing the copy of pointer, so it still points to that object)

![stack](../image/passByValue.png)

###final keyword
- final, variable can only be assigned once
- is similar to const in C
```
final Customer c= new Customer("John");
c = new Customer("Susan"); //compile error

```

###Escaping reference
- if we add ```records.clear()``` at end of this code, then it will clear the records
- it will work like this CustomerRecords is defined public instead of private, since we can direcly operate on them
- one solution is that we make this CustomerRecords directly iterable

![stack](../image/escapingReference.png)
![stack](../image/escapingReferenceSolution.png)

####Better way
- Still, it's not perfect way since iterator also has a remove method
- a better way is to return a new hashmap using constructor like below
- then we are not allowed to edit original object without setter
- so even we do ```records.getCustomers.clear()```, it wont impact on original object

![stack](../image/escapingReferenceSolution2.png)

####Improvement
- the safe way is to return immutable collections
- make it unmodifiable

![stack](../image/escapingReferenceSolution3.png)

####Addition
- not even return original objects
- give it a new constructor and return a new object so that no edition will be on original objects
![stack](../image/escapingReferenceSolution4.png)
