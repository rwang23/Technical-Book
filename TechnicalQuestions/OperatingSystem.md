##系统及其它
ACID/CAP 分布式系统
###ACID and CAP
####ACID
- Atomicity: either all occur, or nothing occurs
- Consistency: Any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers
- Isolation: isolation determines how transaction integrity is visible to other users and systems. For example, when a user is creating a Purchase Order and has created the header, but not the Purchase Order lines, is the header available for other systems/users, carrying out concurrent operations (such as a report on Purchase Orders), to see?
- Durability: guarantees that transactions that have committed will survive permanently. For example, if a flight booking reports that a seat has successfully been booked, then the seat will remain booked even if the system crashes.

####CAP
- Consistency (All Nodes Have Same Data via Eventual Consistency)
- Availability
- Partition-Tolerance : system continues to operate despite arbitrary message loss or failure of part of the system

####Difference
CAP theorem: specifies that a distributed system can provide two services (ex. Availability and Partition tolerance) but never three. If for example, a service provides Availability and Partitioning it can never ensure Consistency, not immediately, thus Eventual Consistency is used, which allows the infrastructure to flux between inconsistency and consistency, however at one point, sooner or later, the infrastructure will become consistent, resulting in eventual consistency. Cloud services work in such fashion and Amazon's Simple DB uses eventual consistency.

ACID features are usually applied to relational DBs. If you want to apply ACID in a distributed fashion (distributed DB), ACID uses 2PC(two-phase commit) to force consistency across partitions. However since ACID provides consistency and partitioning, applying the CAP theorem for (distributed environments) this will mean that availability is compromised.

Because of this, BASE (Basically available, soft state, eventually consistent) is used which can provide levels of scalability that cannot be obtained with ACID.


##Multi-Threading
[Intro to multi-threading](http://beginnersbook.com/2013/03/multithreading-in-java/)
####Basic function
	getName(): It is used for Obtaining a thread’s name
	getPriority(): Obtain a thread’s priority
	isAlive(): Determine if a thread is still running
	join(): Wait for a thread to terminate
	run(): Entry point for the thread
	sleep(): suspend a thread for a period of time
	start(): start a thread by calling its run() method
####

Java多线程： extend Tread类，Implement Runnable接口/blockingqueue

###Multi-Threading condition
- In multitasking systems, some abnormal conditions prevent progress of executing processes or threads. I'll refer to both processes and threads simply as "processes". Two of these conditions are called dead-lock and live-lock.
- The former refers to processes which are blocking each other, thus preventing either from executing. The latter refers to processes which prevent each other from progressing, but do not actually block the execution. For instance, they might continually cause each other to rollback transactions, neither ever being able to finish them.
- Another condition is known as resource starvation, in which one or more finite resources, required for the progress of the processes, have been depleted by them and can't be restored unless the processes progress. This is also a special case of live-lock.

###Starvation and Livelock
[Starvation](http://www.math.uni-hamburg.de/doc/java/tutorial/essential/threads/deadlock.html)
[Starvation](https://www.safaribooksonline.com/library/view/erlang-programming/9780596803940/ch04s10.html)
[Starvation](https://codingarchitect.wordpress.com/2006/01/18/multi-threading-basics-deadlocks-livelocks-and-starvation/)
[Starvation](https://richardbarabe.wordpress.com/2014/02/21/java-deadlock-livelock-and-lock-starvation-examples/)
Starvation and livelock are much less common a problem than deadlock, but are still problems that every designer of concurrent software is likely to encounter.

####Starvation
Starvation describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress. This happens when shared resources are made unavailable for long periods by "greedy" threads. For example, suppose an object provides a synchronized method that often takes a long time to return. If one thread invokes this method frequently, other threads that also need frequent synchronized access to the same object will often be blocked.

####Livelock
A thread often acts in response to the action of another thread. If the other thread's action is also a response to the action of another thread, then livelock may result. As with deadlock, livelocked threads are unable to make further progress. However, the threads are not blocked — they are simply too busy responding to each other to resume work. This is comparable to two people attempting to pass each other in a corridor: Alphonse moves to his left to let Gaston pass, while Gaston moves to his right to let Alphonse pass. Seeing that they are still blocking each other, Alphone moves to his right, while Gaston moves to his left. They're still blocking each other, so..

###
序列化的几种方式：JSON／Object Serialize／ProtoBuf

###
what is dead lock?死锁问题／如何解决

###
Design Pattern 设计模式（singleton，factory, builder, decorator）

###
Linux command: kill -9   / scp / telnet / ps
