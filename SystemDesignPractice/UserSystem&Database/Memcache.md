##Memcache

	Description
	Implement a memcache which support the following features:

	get(curtTime, key). Get the key's value, return 2147483647 if key does not exist.
	set(curtTime, key, value, ttl). Set the key-value pair in memcache with a time to live (ttl). The key will be valid from curtTime to curtTime + ttl - 1 and it will be expired after ttl seconds. if ttl is 0, the key lives forever until out of memory.
	delete(curtTime, key). Delete the key.
	incr(curtTime, key, delta). Increase the key's value by delta return the new value. Return 2147483647 if key does not exist.
	decr(curtTime, key, delta). Decrease the key's value by delta return the new value. Return 2147483647 if key does not exist.
	It's guaranteed that the input is given with increasingcurtTime.

##Notes

	Clarification
	Actually, a real memcache server will evict keys if memory is not sufficient, and it also supports variety of value types like string and integer. In our case, let's make it simple, we can assume that we have enough memory and all of the values are integers.

##Examples

	Example
	get(1, 0)
	>> 2147483647
	set(2, 1, 1, 2)
	get(3, 1)
	>> 1
	get(4, 1)
	>> 2147483647
	incr(5, 1, 1)
	>> 2147483647
	set(6, 1, 3, 0)
	incr(7, 1, 1)
	>> 4
	decr(8, 1, 1)
	>> 3
	get(9, 1)
	>> 3
	delete(10, 1)
	get(11, 1)
	>> 2147483647
	incr(12, 1, 1)
	>> 2147483647

##解法
- 写的比较规范,还有getter和setter,虽然没必要

```java
public class Memcache {

    private Map<Integer, KeyNode> memCache;

    private class KeyNode {
        private int curtTime;
        private int value;
        private int endTime;

        KeyNode(int curtTime, int value, int endTime) {
            this.curtTime = curtTime;
            this.value = value;
            this.endTime = endTime;
        }

        public int getCurTime() {
            return this.curtTime;
        }

        public int getValue() {
            return this.value;
        }

        public int getEndTime() {
            return this.endTime;
        }

        public void setCurTime(int curtTime) {
            this.curtTime = curtTime;
        }

        public void setValue(int value) {
            this.value = value;
        }

        public void setEndTime(int endTime) {
            this.endTime = endTime;
        }
    }

    public Memcache() {
        // do intialization if necessary
        memCache = new HashMap<Integer, KeyNode>();

    }

    /*
     * @param curtTime: An integer
     * @param key: An integer
     * @return: An integer
     */
    public int get(int curtTime, int key) {
        // write your code here
        if (!memCache.containsKey(key)) {
            return 2147483647;
        }

        KeyNode node = memCache.get(key);

        if (curtTime >= node.getEndTime() && node.getEndTime() != 0) {
            memCache.remove(key);
            return 2147483647;
        }

        return node.value;
    }

    /*
     * @param curtTime: An integer
     * @param key: An integer
     * @param value: An integer
     * @param ttl: An integer
     * @return: nothing
     */
    public void set(int curtTime, int key, int value, int ttl) {
        // write your code here
        int endTime = 0;
        if (ttl != 0) {
            endTime = curtTime + ttl;
        }

        KeyNode keyNode = new KeyNode(curtTime, value, endTime);
        memCache.put(key, keyNode);

    }

    /*
     * @param curtTime: An integer
     * @param key: An integer
     * @return: nothing
     */
    public void delete(int curtTime, int key) {
        // write your code here
        if (memCache.containsKey(key)) {
            memCache.remove(key);
        }
    }

    /*
     * @param curtTime: An integer
     * @param key: An integer
     * @param delta: An integer
     * @return: An integer
     */
    public int incr(int curtTime, int key, int delta) {
        // write your code here
        int newValue =  2147483647;
        if (memCache.containsKey(key)) {
            KeyNode node = memCache.get(key);

            if (curtTime > node.getEndTime() && node.getEndTime() != 0) {
                memCache.remove(key);
                return 2147483647;
            }

            newValue = node.getValue() + delta;
            node.setValue(newValue);
        }

        return newValue;
    }

    /*
     * @param curtTime: An integer
     * @param key: An integer
     * @param delta: An integer
     * @return: An integer
     */
    public int decr(int curtTime, int key, int delta) {
        // write your code here
        int newValue =  2147483647;
        if (memCache.containsKey(key)) {
            KeyNode node = memCache.get(key);

            if (curtTime > node.getEndTime() && node.getEndTime() != 0) {
                memCache.remove(key);
                return 2147483647;
            }

            newValue = node.getValue() - delta;
            node.setValue(newValue);
        }
        return newValue;
    }
}
```
