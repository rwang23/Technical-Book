###队列在工业界的应用
队列可用于实现消息队列（message queue），以完成异步（asynchronous）任务。

“消息”是计算机间传送的数据，可以只包含文本；也可复杂到包含嵌入对象。当消息“生产”和“消费”的速度不一致时，就需要消息队列，临时保存那些已经发送而并未接收的消息。例如集体打包调度，服务器繁忙时的任务处理，事件驱动等等。

常用的消息队列实现包括RabbitMQ，ZeroMQ等等。

[为什么需要消息队列，及使用消息队列的好处？](http://www.ywnds.com/?p=5791)
[RabbitMQ的应用场景以及基本原理介绍](http://blog.csdn.net/whoamiyang/article/details/54954780)
