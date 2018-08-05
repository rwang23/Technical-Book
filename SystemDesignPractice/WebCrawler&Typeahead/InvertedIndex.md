##Inverted Index

	Create an inverted index with given documents.

	Example
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
- 这道题就是理解什么是Inverted index
- 有道相同的题 要求使用map reduce来做这道题

```java
/**
 * Definition of Document:
 * class Document {
 *     public int id;
 *     public String content;
 * }
 */
public class Solution {
    /**
     * @param docs a list of documents
     * @return an inverted index
     */
    public Map<String, List<Integer>> invertedIndex(List<Document> docs) {
        // Write your code here
        Map<String, List<Integer>> invertedIndexMap = new HashMap<String, List<Integer>>();

        if (docs == null || docs.size() == 0) {
            return invertedIndexMap;
        }

        for (Document doc : docs) {
            String[] words = doc.content.split("\\s+");
            for (int i = 0; i < words.length; i++) {

                if (invertedIndexMap.containsKey(words[i]) ) {
                    List list =  invertedIndexMap.get(words[i]);
                    if ((Integer)list.get(list.size() - 1) != doc.id) {
                        list.add(doc.id);
                    }
                } else {
                    List<Integer> docIDList = new ArrayList<Integer>();
                    docIDList.add(doc.id);
                    invertedIndexMap.put(words[i], docIDList);
                }
            }

        }

        return invertedIndexMap;
    }
}
```

