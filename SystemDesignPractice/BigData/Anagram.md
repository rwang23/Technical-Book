##Anagram (Map Reduce)
	Use Map Reduce to find anagrams in a given list of words.

##Example
	Given ["lint", "intl", "inlt", "code"], return ["lint", "inlt", "intl"],["code"].

	Given ["ab", "ba", "cd", "dc", "e"], return ["ab", "ba"], ["cd", "dc"], ["e"].

##思路

```java
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 */
public class Anagram {

    public static class Map {
        public void map(String key, String value,
                        OutputCollector<String, String> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, String value);
            String[] strings = value.split("\\s");

            for (int i = 0; i < strings.length; i++) {
                char[] array = strings[i].toCharArray();
                Arrays.sort(array);
                String pattern = new String(array);
                output.collect(pattern, strings[i]);
            }
        }
    }

    public static class Reduce {
        public void reduce(String key, Iterator<String> values,
                           OutputCollector<String, List<String>> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, List<String> value);
            List<String> result = new ArrayList<String>();
            while (values.hasNext()){
                String next = values.next();
                result.add(next);
            }
            output.collect(key, result);
        }
    }
}

```
