##Typeahead
[lintcode](https://www.lintcode.com/problem/typeahead/description)

##Description

	Implement typeahead. Given a string and a dictionary, return all words that contains the string as a substring.
	The dictionary will give at the initialize method and wont be changed.
	The method to find all words with given substring would be called multiple times.

##Example

	Given dictionary = {"Jason Zhang", "James Yu", "Bob Zhang", "Larry Shi"}

	search "Zhang", return ["Jason Zhang", "Bob Zhang"].

	search "James", return ["James Yu"].

	search "ang", return ["Jason Zhang", "Bob Zhang"].

##思路
- 对每个单词建立倒排索引,并且对每个单词的substring也建立倒排索引
- 但是只通过了50%case

```java
public class Typeahead {
    /*
    * @param dict: A dictionary of words dict
    */

    Map<String, List<Integer>> dictMap = new HashMap<String, List<Integer>>();
    Map<Integer, String> idToString = new HashMap<Integer, String>();

    public Typeahead(Set<String> dict) {
        // do intialization if necessary
        dictMap = invertedIndex(dict);
    }

    /*
     * @param str: a string
     * @return: a list of words
     */
    public List<String> search(String str) {
        // write your code here
        List<String> result = new ArrayList<String>();
        if (dictMap.containsKey(str)) {
            List<Integer> list = dictMap.get(str);
            for (Integer i : list) {
                result.add(idToString.get(i));
            }
        }
        return result;
    }

    public Map<String, List<Integer>> invertedIndex(Set<String> docs) {
        // Write your code here

        Map<String, List<Integer>> invertedIndexMap = new HashMap<String, List<Integer>>();

        if (docs == null || docs.size() == 0) {
            return invertedIndexMap;
        }

        int id = 0;
        for (String doc : docs) {
            idToString.put(id, doc);
            String[] words = doc.split("\\s+");
            for (int i = 0; i < words.length; i++) {
                String word = words[i];
                buildIndexMap(invertedIndexMap, word, id);
                List<String> innerWords = generateSubstring(word);
                for (String inner : innerWords) {
                    buildIndexMap(invertedIndexMap, inner, id);
                }
            }
            id++;
        }

        return invertedIndexMap;
    }

    public void buildIndexMap(Map<String, List<Integer>> invertedIndexMap, String word, int id) {

        if (invertedIndexMap.containsKey(word)) {
            List list =  invertedIndexMap.get(word);
            if ((Integer)list.get(list.size() - 1) != id) {
                list.add(id);
            }
        } else {
            List<Integer> docIDList = new ArrayList<Integer>();
            docIDList.add(id);
            invertedIndexMap.put(word, docIDList);
        }
    }

    public List<String> generateSubstring(String string) {
        List<String> result = new ArrayList<String>();
        int length = string.length();
        for (int i = 0; i < length; i++) {
            for (int j = i + 1; j <= length; j++) {
                String subString = string.substring(i,j);
                result.add(subString);
            }
        }
        return result;
    }
}
```

##思路
- 其实只需要建立map<substring, string>, 不需要依靠ID

```java
public class Typeahead {
    private HashMap<String, List<String>> map = new HashMap<String , List<String>>();
    // @param dict A dictionary of words dict
    public Typeahead(Set<String> dict) {
        // do initialize if necessary
        for (String str : dict) {
            int len = str.length();
            for (int i = 0; i < len; ++i)
                for (int j = i + 1; j <= len; ++j) {
                    String tmp = str.substring(i, j);
                    if (!map.containsKey(tmp)) {
                        map.put(tmp, new ArrayList<String>());
                        map.get(tmp).add(str);
                    } else {
                        List<String> index = map.get(tmp);
                        if (!str.equals(index.get(index.size() - 1))) {
                            index.add(str);
                        }
                    }
                }
        }
    }

    // @param str: a string
    // @return a list of words
    public List<String> search(String str) {
        // Write your code here
        if (!map.containsKey(str)) {
            return new ArrayList<String>();
        } else {
            return map.get(str);
        }
    }
}
```
