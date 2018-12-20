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

###Scale
