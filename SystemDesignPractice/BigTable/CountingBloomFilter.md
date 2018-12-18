##Counting Bloom Filter
[lintcode](https://www.lintcode.com/problem/counting-bloom-filter/description)
	Implement a counting bloom filter. Support the following method:

	add(string). Add a string into bloom filter.
	contains(string). Check a string whether exists in bloom filter.
	remove(string). Remove a string from bloom filter.
##Example

	CountingBloomFilter(3)
	add("lint")
	add("code")
	contains("lint") // return true
	remove("lint")
	contains("lint") // return false

##思路
- 比standard多了remove
- 因为要remove,所以使用int数组,而不是bitset的boolean数组
- 当删除的时候,int减1,如果等于0,那就意味着彻底删除了.
- 误区:千万不要用hashmap,用bloomfilter的一个目的就是为了省空间


```java
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

public class CountingBloomFilter {

    public int[] bits;
    public int k;
    public List<HashFunction> hashFunc;

    public CountingBloomFilter(int k) {
        // initialize your data structure here
        this.k = k;
        hashFunc = new ArrayList<HashFunction>();
        for (int i = 0; i < k; ++i)
            hashFunc.add(new HashFunction(100000 + i, 2 * i + 3));
        bits = new int[100000 + k];
    }

    public void add(String word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc.get(i).hash(word);
            bits[position] += 1;
        }
    }

    public void remove(String word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc.get(i).hash(word);
            bits[position] -= 1;
        }
    }

    public boolean contains(String word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc.get(i).hash(word);
            if (bits[position] <= 0)
                return false;
        }
        return true;
    }
}
```
