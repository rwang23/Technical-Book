##Type Ahead

![TypeAhead](../image/TypeAhead.png)

Google suggestion:
Prefix -> top n hot key Words
Twitter typeahead:
Suggestion + user + hashtag

###Scenario
- DAU = 500M
- SEARCH 4 * 6 * 500 = 12B every user searches 6 times and types 4 letters
- QPS = 12b / 86400 = 138k
- Peak QPS = 300k

###Service
![typeaheadService](../image/typeaheadService.png)

![typeAheadQuery](../image/typeAheadQuery.png)
- 可以稍微作修改,存一个prefix作为key, value就存对应的keywords,就会好一点
- 继续优化的话,我们更改使用trie
- 继续优化,把每个字母节点上的count存在每个节点上
- 继续优化,在节点上储存top n hot key words

![typeAheadTrie](../image/typeAheadTrie.png)


####Data collection Service 如何进行统计,搜索如何得到数据的

![typeAheadDataCollectionService](../image/typeAheadDataCollectionService.png)

###Storage
- Query Service: in-memory trie along with disk serialization
- DataCollectionService: Big Table

###Scale
- 两个重要指标: reponse time 和 result quality

####减少response times
#####减少front-end (browser) response time
- cache result (local storage, 因为结果不会经常发生变化)
- prefetch (比如:当输入pin的时候,已经把pink pint ping的结果发给browser了 )

####what if the trie get too large for one machine
- We use consistent hashing to decide which machine a particular string belongs to
![consistentHashingTrie](../image/consistentHashingTrie.png)

####How to reduce the size of log file
- 不可能去查询所有记录,比如有20b条搜索,不能去搜一遍
- probabilistic logging, 按照1/10000概率去记录,去统计搜索次数
