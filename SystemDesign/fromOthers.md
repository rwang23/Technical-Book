##语言知识点：以java为例
###Java 语言特性Java 以及 c ++ 区别;
####abstract class vs interface
- Interface in Java can only contains declaration. You can not declare any concrete methods inside interface. On the other hand abstract class may contain both abstract and concrete methods, which makes abstract class an ideal place to provide common or default functionality.
- You can implement multiple interface but can only extends one abstract, Which means interface can provide more Polymorphism support than abstract class .
- In order to implement interface in Java, you need to provide implementation of all methods, which is very painful. On the other hand abstract class may help you in this case by providing default implementation.

####shallow copy/deep copy
- Shallow copies duplicate as little as possible. A shallow copy of a collection is a copy of the collection structure, not the elements. With a shallow copy, two collections now share the individual elements.
- Deep copies duplicate everything. A deep copy of a collection is two collections with all of the elements in the original collection duplicated.


####pass by reference/ pass by value;
- Pass by value - The function copies the variable and works with a copy(so it doesn't change anything in the original variable)
- Pass by reference - The function uses the original variable, if you change the variable in the other function, it changes in the original variable too.
- Java only pass by value but C++ can pass by value and also reference

####hashcode()/ equals()
- hashCode() method returns an int hash value corresponding to an object. It's used in hash based collection classes e.g Hashtable, HashMap, LinkedHashMap and so on. It's very tightly related to equals() method. According to Java specification, two objects which are equal to each other using equals() method must have same hash code.


####Difference between final, finalize and finally?
- The final is a modifier which you can apply to variable, methods and classes. If you make a variable final it means its value cannot be changed once initialized.
- finalize is a method, which is called just before an object is a garbage collected, giving it last chance to resurrect itself, but the call to finalize is not guaranteed.
- finally is a keyword which is used in exception handling along with try and catch. the finally block is always executed irrespective of whether an exception is thrown from try block or not.

####Static
- static members belong to the class instead of a specific instance.
- It means that only one instance of a static field exists[1] even if you create a million instances of the class or you don't create any. It will be shared by all instances.
- Since static methods also do not belong to a specific instance, they can't refer to instance members. static members can only refer to static members. Instance members can, of course access static members

####checked/unchecked exception
- checked exception is checked by the compiler at compile time. It's mandatory for a method to either handle the checked exception or declare them in their throws clause.
- The unchecked exception is the descendant of RuntimeException and not checked by the compiler at compile time.


####java 8种primitive type
- byle 8 bit
- short 16 bit
- int 32 bit
- long 64 bit
- float 32 bit
- double 64 bit
- char 16 bit unicode
- boolean i bit

####overloading vs overriding；
- First and major difference between Overloading and Overriding is that former occur during compile time while later occur during runtime.
- Second difference between Overloading and Overriding is that, you can overload method in same class but you can only override method in sub class.
- Third difference is that you can overload static method in Java but you can not override static method in Java. In fact when you declare same method in Sub Class it's known as method hiding because it hide super class method instead of overriding it.


#### public static void main(string args[])每个关键字的作用
- A private member is only accessible within the same class as it is declared.
- A member with no access modifier is only accessible within classes in the same package.
- A protected member is accessible within all classes in the same package and within subclasses in other packages.
- A public member is accessible to all classes (unless it resides in a module that does not export the package it is declared in).

####What is the difference between stack and heap in Java? (answer)
- Stack and heap are different memory areas in the JVM and they are used for different purposes.
- The stack is used to hold method frames and local variables while objects are always allocated memory from the heap.
- The stack is usually much smaller than heap memory and also didn't shared between multiple threads, but heap is shared among all threads in JVM.

##Java Collections：
####stack/queue/deque;
- A stack is a last in, first out (LIFO) data structure. Items are removed from a stack in the reverse order from the way they were inserted
- A queue is a first in, first out (FIFO) data structure. Items are removed from a queue in the same order as they were inserted
- A deque is a double-ended queue, items can be inserted and removed at either end

####hashset/treeset
- HashSet is Implemented using a hash table. Elements are not ordered. The add, remove, and contains methods have constant time complexity O(1).
- TreeSet is implemented using a tree structure(red-black tree in algorithm book). The elements in a set are sorted, but the add, remove, and contains methods has time complexity of O(log (n)). It offers several methods to deal with the ordered set like first(), last(), headSet(), tailSet(), etc.
- LinkedHashSet is between HashSet and TreeSet. It is implemented as a hash table with a linked list running through it, so it provides the order of insertion. The time complexity of basic methods is O(1).


- String vs StringBuffer;
- Hashmap/TreeMap/Hashtable/LinkedHashMap/ ConcurrentHashMap;
- Array/ArrayList/LinkedList;
- PriorityQueue(heap);
- comparable/comparator; iterator


###拓展一些问题： Java memory leak/JVM/ garbage collection,  Object class method: getclass()/ hashcode(); java: heap/stack存什么; Java 8/Java 7

##数据结构和算法
	二叉树：超级重点： 收集所有二叉树的题
	链表： 会翻转／快慢指针
	Binary Deduction/Search: sorted/rotated array/ Sqrt()
	实现基本数据结构： hashmap， stack和queue
	Array/ String： shuffle an array， java big integer实现
	dfs vs bfs  word ladder/ topological  sorting
	简单dp，不需要很复杂: paint house/stock price/


##计算机网络
1. TCP 三次握手，TCP/UDP 区别；
2.  http/https 区别；http request：post／get ；http port 80 ssl;
3.输入www.google.com 会发生什么；What happens when you type [url]www.google.com in your browser?[/url]
4.Public key/Private key;
5. HTTP 401, 403, or 404 Error／ client/server模型


##数据库
1. SQL vs NoSql 区别
2. select／update／delete／insert
3.primary key；join（四种）和index 原理和作用
4.简单的sql语句：从table中找出成绩第二好的学生姓名； group by
5.简单了解几种nosql数据库： MangoDB/ Cassandra/HBase


##系统及其它
ACID/CAP 分布式系统
Java多线程： extend Tread类，Implement Runnable接口/blockingqueue
序列化的几种方式：JSON／Object Serialize／ProtoBuf
what is dead lock?死锁问题／如何解决
Design Pattern 设计模式（singleton，factory, builder, decorator）
Linux command: kill -9   / scp / telnet / ps
