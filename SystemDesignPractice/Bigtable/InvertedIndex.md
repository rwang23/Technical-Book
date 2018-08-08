##Inverted Index
[lintcode](https://www.lintcode.com/problem/inverted-index/description?source=ladder)

  Create an inverted index with given documents.

##Example

  Given a list of documents with id and content. (class Document)

  [
    {
      "id": 1,
      "content": "This is the content of document 1 it is very short"
    },
    {
      "id": 2,
      "content": "This is the content of document 2 it is very long bilabial bilabial heheh hahaha ..."
    },
  ]
  Return an inverted index (HashMap with key is the word and value is a list of document ids).

  {
     "This": [1, 2],
     "is": [1, 2],
     ...
  }
  Notice
  Ensure that data does not include punctuation.

##思路
```java
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 * Definition of Document:
 * class Document {
 *     public int id;
 *     public String content;
 * }
 */
public class InvertedIndex {

    public static class Map {
        public void map(String _, Document value,
                        OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, int value);
        }
    }

    public static class Reduce {
        public void reduce(String key, Iterator<Integer> values,
                           OutputCollector<String, List<Integer>> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, List<Integer> value);
        }
    }
}
```

