##Implement Trie (Prefix Tree)
[lintcode](https://www.lintcode.com/en/problem/implement-trie-prefix-tree/)

##Description
	Implement a trie with insert, search, and startsWith methods.

	You may assume that all inputs are consist of lowercase letters a-z.

##Example
	insert("lintcode")
	search("code")
	>>> false
	startsWith("lint")
	>>> true
	startsWith("linterror")
	>>> false
	insert("linterror")
	search("lintcode)
	>>> true
	startsWith("linterror")
	>>> true

##思路
- 知道了trie的定义的话,这个题很简单
- 用了两种方法
- 一种使用了数组
- 一种使用了hashmap
- 用了递归，其实并不需要递归，一个for循环就行了, for 循环参考trie service


##数组
```java

public class Trie {

    Node parent;
    public Trie() {
        // do intialization if necessary
        parent = new Node();
    }

    public final static int R = 256;

    public class Node {
        Node[] next;
        boolean isWord;
        public Node() {
            next = new Node[R];
            isWord = false;
        }
    }


    public void insert(String word) {
        // write your code here
        insert(parent, word, 0);

    }

    public Node insert(Node node, String word, int index) {
        if (node == null) {
            node = new Node();
        }

        if (word.length() == index) {
            node.isWord = true;
            return node;
        }

        char c = word.charAt(index);
        node.next[c] = insert(node.next[c], word, index + 1);
        return node;
    }


    public boolean search(String word) {
        // write your code here
        return search(parent, word, 0, false);
    }

    public boolean search(Node node, String word, int index, boolean startWith) {
        // write your code here
        if (node == null) {
            return false;
        }

        if (word.length() == index) {
            if (!startWith && node.isWord) {
                return true;
            } else if (startWith) {
                return true;
            } else {
                return false;
            }
        }

        char c = word.charAt(index);
        return search(node.next[c], word, index + 1, startWith);

    }


    public boolean startsWith(String prefix) {
        // write your code here
        return search(parent, prefix, 0, true);
    }
}
```

##hashmap
```java

public class Trie {
    Node root;
    public Trie() {
        // do intialization if necessary
        root = new Node();
    }

    public class Node {
        Map<Character, Node> next;
        boolean isWord;
        public Node() {
            next = new HashMap<Character, Node>();
            isWord = false;
        }
    }
    /*
     * @param word: a word
     * @return: nothing
     */
    public void insert(String word) {
        // write your code here
        insert(root, word, 0);

    }

    public Node insert(Node node, String word, int index) {
        if (node == null) {
            node = new Node();
        }

        if (word.length() == index) {
            node.isWord = true;
            return node;
        }

        char c = word.charAt(index);
        if(!node.next.containsKey(c)) {
            node.next.put(c, new Node());
        }
        insert(node.next.get(c), word, index + 1);
        return node;
    }

    /*
     * @param word: A string
     * @return: if the word is in the trie.
     */
    public boolean search(String word) {
        // write your code here
        return search(root, word, 0, false);
    }

    public boolean search(Node node, String word, int index, boolean startWith) {
        // write your code here
        if (node == null) {
            return false;
        }

        if (word.length() == index) {
            if (!startWith && node.isWord) {
                return true;
            } else if (startWith) {
                return true;
            } else {
                return false;
            }
        }

        char c = word.charAt(index);
        return search(node.next.get(c), word, index + 1, startWith);

    }

    /*
     * @param prefix: A string
     * @return: if there is any word in the trie that starts with the given prefix.
     */
    public boolean startsWith(String prefix) {
        // write your code here
        return search(root, prefix, 0, true);
    }
}
```
