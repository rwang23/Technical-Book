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



Java多线程： extend Tread类，Implement Runnable接口/blockingqueue
序列化的几种方式：JSON／Object Serialize／ProtoBuf
what is dead lock?死锁问题／如何解决
Design Pattern 设计模式（singleton，factory, builder, decorator）
Linux command: kill -9   / scp / telnet / ps
