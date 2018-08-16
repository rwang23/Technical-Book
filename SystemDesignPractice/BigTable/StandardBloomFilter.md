##Standard Bloom Filter
	Implement a standard bloom filter. Support the following method:

	StandardBloomFilter(k),The constructor and you need to create k hash functions.
	add(string). add a string into bloom filter.
	contains(string). Check a string whether exists in bloom filter.

##Example
	StandardBloomFilter(3)
	add("lint")
	add("code")
	contains("lint") // return true
	contains("world") // return false

##思路
- 使用了[BitSet](https://www.geeksforgeeks.org/bitset-class-java-set-1/) Class
- hash 一个数值
- 自己写的hash还不够好,应该加入seed,更随机
- 参考第二个程序

```java
public class StandardBloomFilter {

    List<BitSet> list = new ArrayList<BitSet>();
    int k = 0;
    /*
    * @param k: An integer
    */
    public StandardBloomFilter(int num) {
        // do intialization if necessary
        for (int i = 0; i < num; i++) {
            BitSet bs = new BitSet(10000 + i);
            list.add(bs);
        }
        k = num;
    }

    /*
     * @param word: A string
     * @return: nothing
     */
    public void add(String word) {
        // write your code here
        int hash = hash(word);
        for (int i = 0; i < k; i++) {
            int index = hash % (10000 + i);

            BitSet bs = list.get(i);
            bs.set(index);
        }
    }

    /*
     * @param word: A string
     * @return: True if contains word
     */
    public boolean contains(String word) {
        // write your code here
        int hash = hash(word);
        System.out.println(hash);
        for (int i = 0; i < k; i++) {
            int index = hash % (10000 + i);
            BitSet bs = list.get(i);
            System.out.println(index);
            boolean b1 = bs.get(index);

            if (!(b1)) {
                return false;
            }
        }

        return true;

    }

    public int hash(String word) {
        if (word == null || word.equals("")) {
            return 0;
        }
        int hash = 0;
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            hash = hash * 43 + (c - '0');
        }

        if (hash < 0) {
            return -hash;
        }
        return hash;
    }
}
```

##更好的答案


```java
import java.util.BitSet;

class HashFunction {
    public int cap, seed;

    public HashFunction(int cap, int seed) {
        this.cap = cap;
        this.seed = seed;
    }

    public int hash(String value) {
        int ret = 0;
        int n = value.length();
        for (int i = 0; i < n; ++i) {
            ret += seed * ret + value.charAt(i);
            ret %= cap;
        }
        return ret;
    }
}

public class StandardBloomFilter {

    public BitSet bits;
    public int k;
    public List<HashFunction> hashFunc;

    public StandardBloomFilter(int k) {
        // initialize your data structure here
        this.k = k;
        hashFunc = new ArrayList<HashFunction>();
        for (int i = 0; i < k; ++i)
            hashFunc.add(new HashFunction(100000 + i, 2 * i + 3));
        bits = new BitSet(100000 + k);
    }

    public void add(String word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc.get(i).hash(word);
            bits.set(position);
        }
    }

    public boolean contains(String word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc.get(i).hash(word);
            if (!bits.get(position))
                return false;
        }
        return true;
    }
}
```
