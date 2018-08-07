##Trie Serialization

##Description
Serialize and deserialize a trie (prefix tree, search on internet for more details).

You can specify your own serialization algorithm, the online judge only cares about whether you can successfully deserialize the output from your own serialize function.

##Example
	str = serialize(old_trie)
	>> str can be anything to represent a trie
	new_trie = deserialize(str)
	>> new_trie should have the same structure and values with old_trie
	An example of test data: trie tree <a<b<e<>>c<>d<f<>>>>, denote the following structure:

	     root
	      /
	     a
	   / | \
	  b  c  d
	 /       \
	e         f


##思路
- 初一想就是二叉树的serilize,但是这个每次都不知道子节点多少个
- 倒是可以通过递归从左遍历,像二叉树pre-order前序遍历一样
- 既然可以通过DFS,那就应该能BFS,所以想到,能不能层层遍历,获得每个string,然后deserilize的时候,再从新插入string不就行了嘛
- 所以用了一个queue,存父节点,然后再把子节点放入,实现层层遍历,同时维持一个string queue,生成每一层对应的string,最后获得string,加入到一个list of string, 再合并list,得到string
- deserilize就是重新插入获得的string

```java
/**
 * Definition of TrieNode:
 * public class TrieNode {
 *     public NavigableMap<Character, TrieNode> children;
 *     public TrieNode() {
 *         children = new TreeMap<Character, TrieNode>();
 *     }
 * }
 */


class Solution {
    /**
     * This method will be invoked first, you should design your own algorithm
     * to serialize a trie which denote by a root node to a string which
     * can be easily deserialized by your own "deserialize" method later.
     */
    public String serialize(TrieNode root) {
        // Write your code here

        TrieNode node = root;
        Queue<TrieNode> waitingQueue = new LinkedList<TrieNode>();
        Queue<String> waitingString = new LinkedList<String>();
        List<String> results = new ArrayList<String>();
        waitingQueue.offer(node);
        waitingString.offer(new String(""));

        while (!waitingQueue.isEmpty()) {
            node = waitingQueue.poll();
            String string = waitingString.poll();
            NavigableMap<Character, TrieNode> children = node.children;
            for (Map.Entry<Character, TrieNode> entry : children.entrySet()) {
                Character key = entry.getKey();
                TrieNode child = entry.getValue();
                StringBuilder sb = new StringBuilder(string);
                String searchString = sb.append(key).toString();
                if (child.children.isEmpty()) {
                    results.add(searchString);
                } else {
                    waitingQueue.offer(child);
                    waitingString.offer(searchString);
                }
            }
        }

        return makeString(results);
    }

    public String makeString(List<String> list) {
        StringBuilder result = new StringBuilder("");
        if (list == null || list.size() == 0) {
            return result.toString();
        }
        for (String s : list) {
            result.append(s);
            result.append(' ');
        }

        return result.toString();
    }

    /**
     * This method will be invoked second, the argument data is what exactly
     * you serialized at method "serialize", that means the data is not given by
     * system, it's given by your own serialize method. So the format of data is
     * designed by yourself, and deserialize it here as you serialize it in
     * "serialize" method.
     */
    public TrieNode deserialize(String data) {
        // Write your code here
        TrieNode root = new TrieNode();
        if (data == null || data.length() == 0) {
            return root;
        }

        String[] contents = data.split("\\s");
        for (int i = 0; i < contents.length; i++) {
            insert(root, contents[i], 0);
        }

        return root;
    }

    public TrieNode insert(TrieNode node, String word, int index) {
        if (node == null) {
            node = new TrieNode();
        }

        if (word.length() == index) {
            return node;
        }

        char c = word.charAt(index);
        if(!node.children.containsKey(c)) {
            node.children.put(c, new TrieNode());
        }
        insert(node.children.get(c), word, index + 1);
        return node;
    }

}

```
