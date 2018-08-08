##Top K Frequent Words (Map Reduce)
[lintcode](https://www.lintcode.com/problem/top-k-frequent-words-map-reduce/description?source=ladder)

	Find top k frequent words with map reduce framework.

	The mapper's key is the document id, value is the content of the document, words in a document are split by spaces.

	For reducer, the output should be at most k key-value pairs, which are the top k words and their frequencies in this reducer.
	The judge will take care about how to merge different reducers' results to get the global top k frequent words, so you don't need to care about that part.

	The k is given in the constructor of TopK class.

##Example
	Given document A =

	lintcode is the best online judge
	I love lintcode
	and document B =

	lintcode is an online judge for coding interview
	you can test your code online at lintcode
	The top 2 words and their frequencies should be

	lintcode, 4
	online, 3
	Notice
	For the words with same frequency, rank them with alphabet.

##思路
- 这里在reduce里边用了priority queue,是每台机器有自己的priority queue,每个pq都有top k吧,所以在最后输出之后,需要对着n台机器的的n个top k pq进行汇总(如果有,那这个汇总代码应该写在哪里,是server自己去做汇总吗)?
- cleanup的作用是什么? 感觉cleanup的内容也能放在reduce里边呀


```java
class Pair {
    String key;
    int value;

    Pair(String key, int value) {
        this.key = key;
        this.value = value;
    }
}

public class TopKFrequentWords {

    public static class Map {
        public void map(String _, Document value,
                        OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, int value);
            int id = value.id;
            String content = value.content;
            String[] words = content.split(" ");
            for (String word : words)
                if (word.length() > 0) {
                    output.collect(word, 1);
                }
        }
    }

    public static class Reduce {
        private PriorityQueue<Pair> Q = null;
        private int k;

        private Comparator<Pair> pairComparator = new Comparator<Pair>() {
            public int compare(Pair left, Pair right) {
                if (left.value != right.value) {
                    return left.value - right.value;
                }
                return right.key.compareTo(left.key);
            }
        };

        public void setup(int k) {
            // initialize your data structure here
            this.k = k;
            Q = new PriorityQueue<Pair>(k, pairComparator);
        }

        public void reduce(String key, Iterator<Integer> values) {
            // Write your code here
            int sum = 0;
            while (values.hasNext()) {
                    sum += values.next();
            }

            Pair pair = new Pair(key, sum);
            if (Q.size() < k) {
                Q.add(pair);
            } else {
                Pair peak = Q.peek();
                if (pairComparator.compare(pair, peak) > 0) {
                    Q.poll();
                    Q.add(pair);
                }
            }
        }

        public void cleanup(OutputCollector<String, Integer> output) {
            // Output the top k pairs <word, times> into output buffer.
            // Ps. output.collect(String key, Integer value);
            List<Pair> pairs = new ArrayList<Pair>();
            while (!Q.isEmpty()) {
                pairs.add(Q.poll());
            }

            // reverse result
            int n = pairs.size();
            for (int i = n - 1; i >= 0; --i) {
                Pair pair = pairs.get(i);
                output.collect(pair.key, pair.value);
            }
        }
    }
}
```
