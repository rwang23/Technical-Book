##External Sort
[From wiki](https://en.wikipedia.org/wiki/External_sorting)
External merge sort

One example of external sorting is the external merge sort algorithm, which sorts chunks that each fit in RAM, then merges the sorted chunks together. For example, for sorting 900 megabytes of data using only 100 megabytes of RAM:

Read 100 MB of the data in main memory and sort by some conventional method, like quicksort.
Write the sorted data to disk.

Repeat steps 1 and 2 until all of the data is in sorted 100 MB chunks (there are 900MB / 100MB = 9 chunks), which now need to be merged into one single output file.

Read the first 10 MB (= 100MB / (9 chunks + 1)) of each sorted chunk into input buffers in main memory and allocate the remaining 10 MB for an output buffer. (In practice, it might provide better performance to make the output buffer larger and the input buffers slightly smaller.)

Perform a 9-way merge and store the result in the output buffer. Whenever the output buffer fills, write it to the final sorted file and empty it. Whenever any of the 9 input buffers empties, fill it with the next 10 MB of its associated 100 MB sorted chunk until no more data from the chunk is available.

This is the key step that makes external merge sort work externally -- because the merge algorithm only makes one pass sequentially through each of the chunks, each chunk does not have to be loaded completely; rather, sequential parts of the chunk can be loaded as needed.

Historically, instead of a sort, sometimes a replacement-selection algorithm[3] was used to perform the initial distribution, to produce on average half as many output chunks of double the length.

##Hashtable
	Hash tables suffer from O(n) worst time complexity due to two reasons:

	1 .If too many elements were hashed into the same key: looking inside this key may take O(n) time.
	2. Once a hash table has passed its load balance - it has to rehash [create a new bigger table, and re-insert each element to the table].

	However, it is said to be O(1) average and amortized case because:

	It is very rare that many items will be hashed to the same key [if you chose a good hash function and you don't have too big load balance.
	The rehash operation, which is O(n), can at most happen after n/2 ops, which are all assumed O(1): Thus when you sum the average time per op, you get : (n*O(1) + O(n)) / n) = O(1)

	Hash Tables suffer from bad cache performance, and thus for large collection - the access time might take longer, since you need to reload the relevant part of the table from the memory back into the cache.

##Recursion VS Iterative
###Pros
- Solutions is often shorter, closer in spirit to abstract mathematical entity.
- Good recursive solutions may be more difficult to design and test.

###Cons
On the downside, it decreases the performance of your code. Recursive functions have to keep the function records in memory and jump from one memory address to another to be invoked to pass parameters and return values. That makes them very bad performance.
which can cause stack overflow especially when there is larger input size

###Differences between HashMap and Hashtable?
- [From](http://stackoverflow.com/questions/40471/differences-between-hashmap-and-hashtable)

####There are several differences between HashMap and Hashtable in Java:

- Hashtable is synchronized, whereas HashMap is not. This makes HashMap better for non-threaded applications, as unsynchronized Objects typically perform better than synchronized ones.
- Hashtable does not allow null keys or values.  HashMap allows one null key and any number of NULL values.
- One of HashMap's subclasses is LinkedHashMap, so in the event that you'd want predictable iteration order (which is insertion order by default), you could easily swap out the HashMap for a LinkedHashMap. This wouldn't be as easy if you were using Hashtable.


##C++ vs Java
they have different design goals.
C++ was designed for `systems and applications programming`, (extending the C programming language. To this procedural programming language designed for efficient execution, C++ has added support for statically typed object-oriented programming, exception handling,scoped resource management, and generic programming, in particular. It also added a standard library which includes generic containers and algorithms.)

Java was created initially as an interpreter for `printing systems` but grew to support `network computing`. (It was once used as the base for the "HotJava" thin client system. It relies on a virtual machine to be secure and highly portable. It is bundled with an extensive library designed to provide a complete abstraction of the underlying platform. Java is a statically typed object-oriented language that uses similar (but incompatible) syntax to C++. It was designed from scratch with the goal of being easy to use and accessible to a wider audience. It includes an extensive documentation called Javadoc).

###Then:
- C++ supports pointers whereas Java does not pointers. (But when many programmers questioned how you can work without pointers, the promoters began saying "Restricted pointers.” So we can say java supports Restricted pointers.)
- Exception and Auto Garbage Collector handling in Java is different because there are no destructors into Java.
- At compilation time Java Source code converts into byte code .The interpreter execute this byte code at run time and gives output .Java is interpreted for the most part and hence platform independent. C++ run and compile using compiler which converts source code into machine level languages so c++ is platefrom dependents
- Java is platform independent language but c++ is depends upon operating system machine etc. C++ source can be platform independent (and can work on a lot more, especially embedeed, platforms), although the generated objects are generally platofrom dependent but there is clang for llvmwhich doesn't have this restriction.
- Java uses compiler and interpreter both and in c++ their is only compiler
- C++ supports operator overloading multiple inheritance but java does not.
- C++ is more nearer to hardware then Java
- Everything (except fundamental types) is an object in Java (Single root hierarchy as everything gets derived from java.lang.Object).
- Java is a similar to C++ but not have all the complicated aspects of C++ (ex: Pointers, templates, unions, operator overloading, structures etc..)
- Java does not support conditional compile (#ifdef/#ifndef type).
- Thread support is built-in Java but not in C++. C++11, the most recent iteration of the C++ programming language does have Thread support though.
- Internet support is built-in Java but not in C++. However c++ has support for socket programming which can be used.
- Java does not support header file, include library files just like C++ .Java use import to include different Classes and methods.
- Java does not support default arguments like C++.
- There is no scope resolution operator :: in Java. It has . using which we can qualify classes with the namespace they came from.
- There is no goto statement in Java.
- Java has method overloading, but no operator overloading just like c++.
- The String class does use the + and += operators to concatenate strings and String expressions use automatic type conversion,
- Java is pass-by-value. C++ can pass by value and pass by reference (http://www.learncpp.com/cpp-tutorial/73-passing-arguments-by-reference/)
- Java does not support unsigned integer.

##What's the difference between ASCII and Unicode?
ASCII defines 128 characters, which map to the numbers 0–127. Unicode defines (less than) 221 characters, which, similarly, map to numbers 0–221 (though not all numbers are currently assigned, and some are reserved).

Unicode is a superset of ASCII, and the numbers 0–128 have the same meaning in ASCII as they have in Unicode. For example, the number 65 means "Latin capital 'A'".

Because Unicode characters don't generally fit into one 8-bit byte, there are numerous ways of storing Unicode characters in byte sequences, such as UTF-32 and UTF-8.
