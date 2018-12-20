#Design Tiny URL

###Scenario
1. 根据 Long URL 生成一个 Short URL: http://www.jiuzhang.com => http://bit.ly/1UIoQB6
![Redirect](../image/Redirect.png)
2. 根据Short URL 找到 Long URL进行跳转
3. 两个需要和面试官确认的问题 1)Long Url 和 Short Url 之间必须是一一对应的关系么? 2)Short Url 长时间没人用需要释放么?

```
1. 询问面试官微博日活跃用户
• 约100M
2. 推算产生一条Tiny URL的QPS
• 假设每个用户平均每天发 0.1 条带 URL 的微博
• Average Write QPS = 100M * 0.1 / 86400 ~ 100
• Peak Write QPS = 100 * 2 = 200
3. 推算点击一条Tiny URL的QPS
• 假设每个用户平均点1个Tiny URL
• Average Read QPS = 100M * 1 / 86400 ~ 1k
• Peak Read QPS = 2k
4. 推算每天产生的新的 URL 所占存储
• 100M * 0.1 ~ 10M 条
• 每一条 URL 长度平均 100 算，一共1G
• 1T 的硬盘可以用 3 年
```
###Service
![Tiny URL Service](../image/TinyURLService.png)

###Storage
- 数据库的选择
```
是否需要支持 Transaction?——不需要。NoSQL +1
• NoSQL不支持Transaction
是否需要丰富的 SQL Query?——不需要。NoSQL +1
• NoSQL的SQL Query不是太丰富
• 也有一些NoSQL的数据库提供简单的SQL Query支持
是否想偷懒?——Tiny URL 需要写的代码并不复杂。NoSQL+1 • 大多数 Web Framework 与 SQL 数据库兼容得很好
• 用SQL比用NoSQL少写很多代码

对QPS的要求有多高?—— 经计算，2k QPS并不高，而且2k读可以用Cache，写很少。SQL +1
• NoSQL 的性能更高
对Scalability的要求有多高?—— 存储和QPS要求都不高，单机都可以搞定。SQL+1
• SQL 需要码农自己写代码来 Scale
还记得Db那节课中怎么做Sharding，Replica的么?
• NoSQL 这些都帮你做了
是否需要Sequential ID?——取决于你用什么算法
• SQL 为你提供了 auto-increment 的 Sequential ID
• 也就是1,2,3,4,5 ...
• NoSQL的ID并不是 Sequential 的
```
###算法
![base62](../image/base62.png)
- 用全局自增ID,一般更常用语单机(可以在自增ID前加入一个参数,比如0ID, 1ID, 作为机器的自增ID)
- 也可以生成一个随机的shortURL,这样就不依赖于自增ID,随机的缺点是随着使用的短网址用得越来越多,会变得越来越慢
- 需要对 shortKey 和 longURL 分别建索引(index)。

```
也可以选用 NoSQL 数据库，但是需要建立两张表(大多数NoSQL数据库不支持二级索引) 以 Cassandra 为例子
第一张表:根据 Long 查询 Short
row_key=longURL, column_key=ShortURL, value=null or timestamp
第二张表:根据 Short 查询 Long
row_key=shortURL, column_key=LongURL, value=null or timestamp
```

###Scale

1. 利用缓存
```
利用缓存提􏰁(Cache Aside) • 缓存里需要存两类数据:
• long to short(生成新 short url 时需要)
• short to long(查询 short url 时需要)
```
2.
