##Trie Service
[lintcode](https://www.lintcode.com/problem/trie-service/description)

##Description
	Build tries from a list of <word, freq> pairs. Save top 10 for each node.

##Example
	Given a list of <word, freq>

	<"abc", 2>
	<"ac", 4>
	<"ab", 9>
	Return <a[9,4,2]<b[9,2]<c[2]<>>c[4]<>>>, and denote the following tree structure:

	         Root
	         /
	       a(9,4,2)
	      /    \
	    b(9,2) c(4)
	   /
	 c(2)

##思路
- 很简单,就是每次要保存高频前10,
- 可以替换最小的,可以排序然后每次替换最后的

```java
/**
 * Definition of TrieNode:
 * public class TrieNode {
 *     public NavigableMap<Character, TrieNode> children;
 *     public List<Integer> top10;
 *     public TrieNode() {
 *         children = new TreeMap<Character, TrieNode>();
 *         top10 = new ArrayList<Integer>();
 *     }
 * }
 */
public class TrieService {

    private TrieNode root = null;

    public TrieService() {
        root = new TrieNode();
    }

    public TrieNode getRoot() {
        // Return root of trie root, and
        // lintcode will print the tree struct.
        return root;
    }

    // @param word a string
    // @param frequency an integer
    public void insert(String word, int frequency) {

        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {

            char c = word.charAt(i);
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
            }

            node = node.children.get(c);

            if (node.top10 == null || node.top10.size() <= 10) {
                node.top10.add(frequency);
            } else {
                node.top10.set(node.top10.size() - 1, frequency);
            }
            Collections.sort(node.top10, Collections.reverseOrder());
        }
    }
 }
```
