##N-Gram (Map Reduce)
[lintcode](https://www.lintcode.com/problem/n-gram-map-reduce/description?source=ladder)

	给出若干字符串和数字 N。用 Map Reduce 的方法统计所有 N-Grams 及其出现次数 。以字母为粒度。

	Example
	Given N = 3
	doc_1: "abcabc"
	doc_2: "abcabc"
	doc_3: "bbcabc"

	The final result should be:

	[
	  "abc": ５,
	  "bbc": 1,
	  "bca": 3,
	  "cba": 3
	]

##思路

```java
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 */
public class NGram {

    public static class Map {
        public void map(String _, int n, String str,
                        OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, Integer value);
            for (int index = 0; index < str.length() - n + 1; ++index) {
                output.collect(str.substring(index, index + n), 1);
            }
        }
    }

    public static class Reduce {
        public void reduce(String key, Iterator<Integer> values,
                           OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, int value);
            int sum = 0;
            while (values.hasNext()) {
                    sum += values.next();
            }
            output.collect(key, sum);
        }
    }
}
```
