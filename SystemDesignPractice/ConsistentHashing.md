##Consistent Hashing

	Description
	一般的数据库进行horizontal shard的方法是指，把 id 对 数据库服务器总数 n 取模，然后来得到他在哪台机器上。这种方法的缺点是，当数据继续增加，我们需要增加数据库服务器，将 n 变为 n+1 时，几乎所有的数据都要移动，这就造成了不 consistent。为了减少这种 naive 的 hash方法(%n) 带来的缺陷，出现了一种新的hash算法：一致性哈希的算法——Consistent Hashing。这种算法有很多种实现方式，这里我们来实现一种简单的 Consistent Hashing。

	将 id 对 360 取模，假如一开始有3台机器，那么让3台机器分别负责0~119, 120~239, 240~359 的三个部分。那么模出来是多少，查一下在哪个区间，就去哪台机器。
	当机器从 n 台变为 n+1 台了以后，我们从n个区间中，找到最大的一个区间，然后一分为二，把一半给第n+1台机器。
	比如从3台变4台的时候，我们找到了第3个区间0~119是当前最大的一个区间，那么我们把0~119分为0~59和60~119两个部分。0~59仍然给第1台机器，60~119给第4台机器。
	然后接着从4台变5台，我们找到最大的区间是第3个区间120~239，一分为二之后，变为 120~179, 180~239。
	假设一开始所有的数据都在一台机器上，请问加到第 n 台机器的时候，区间的分布情况和对应的机器编号分别是多少？

##Notes
	你可以假设 n <= 360. 同时我们约定，当最大区间出现多个时，我们拆分编号较小的那台机器。
	比如0~119， 120~239区间的大小都是120，但是前一台机器的编号是1，后一台机器的编号是2, 所以我们拆分0~119这个区间。

	If the maximal interval is [x, y], and it belongs to machine id z, when you add a new machine with id n, you should divide [x, y, z] into two intervals:

	[x, (x + y) / 2, z] and [(x + y) / 2 + 1, y, n]

	Example
	for n = 1, return

	[
	  [0,359,1]
	]
	represent 0~359 belongs to machine 1.

	for n = 2, return

	[
	  [0,179,1],
	  [180,359,2]
	]
	for n = 3, return

	[
	  [0,89,1]
	  [90,179,3],
	  [180,359,2]
	]
	for n = 4, return

	[
	  [0,89,1],
	  [90,179,3],
	  [180,269,2],
	  [270,359,4]
	]
	for n = 5, return

	[
	  [0,44,1],
	  [45,89,5],
	  [90,179,3],
	  [180,269,2],
	  [270,359,4]
	]

##思路
- 可以利用PriorityQueue
- 合理使用Arrays.asList()能节省不少代码量


##解法一
```java
public class Solution {

    public List<List<Integer>> setup() {
        List<List<Integer>> hashList = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        list.add(0);
        list.add(359);
        list.add(1);
        hashList.add(list);
        return hashList;
    }

    /*
     * @param n: a positive integer
     * @return: n x 3 matrix
     */
    public List<List<Integer>> consistentHashing(int n) {
        // write your code here
        List<List<Integer>> hashList = setup();

        if (n == 1) {
            return hashList;
        }

        for (int i = 1; i < n; i++) {
            hashList = createHashingList(hashList);
        }

        return hashList;
    }

    public  List<List<Integer>> createHashingList(List<List<Integer>> hashingList) {
        if (hashingList == null || hashingList.size() < 1) {
            return new ArrayList<List<Integer>>();
        }

        int index = findMaxGap(hashingList);
        List<List<Integer>> newHashingList = new ArrayList<List<Integer>>();

        for (int i = 0; i < hashingList.size(); i++) {
            List<Integer> splitList = hashingList.get(i);
            int firstIndex = splitList.get(0);
            int lastIndex = splitList.get(1);
            int id = splitList.get(2);
            if (i == index) {
                List<Integer> newSplitList1 = new ArrayList<Integer>();
                List<Integer> newSplitList2 = new ArrayList<Integer>();
                newSplitList1.add(firstIndex);
                newSplitList1.add((firstIndex + lastIndex) / 2);
                newSplitList1.add(id);
                newSplitList2.add((firstIndex + lastIndex) / 2 + 1);
                newSplitList2.add(lastIndex);
                newSplitList2.add(hashingList.size() + 1);
                newHashingList.add(newSplitList1);
                newHashingList.add(newSplitList2);
            } else {
                List<Integer> newSplitList = new ArrayList<Integer>();
                newSplitList.add(firstIndex);
                newSplitList.add(lastIndex);
                newSplitList.add(id);
                newHashingList.add(newSplitList);
            }
        }

        return newHashingList;
    }

    public int findMaxGap(List<List<Integer>> hashingList) {
        if (hashingList == null || hashingList.size() <= 1) {
            return 0;
        }

        int max = 0;
        int maxIndex = 0;

        for (int i = 0; i < hashingList.size(); i++) {
            List<Integer> list = hashingList.get(i);
            int gap = list.get(1) - list.get(0);

            if (gap > max) {
                max = gap;
                maxIndex = i;
            }


            if (gap == max) {
                int prevID = hashingList.get(maxIndex).get(2);
                int currentID = hashingList.get(i).get(2);
                maxIndex = (prevID > currentID) ?  i : maxIndex;
            }


        }

        return maxIndex;
    }

}
```

##优秀解法
```java
public class Solution {
    /*
     * @param n: a positive integer
     * @return: n x 3 matrix
     */
    private class Node {
        int start;
        int end;
        int id;
        Node(int start, int end, int id) {
            this.start = start;
            this.end = end;
            this.id = id;
        }
    }
    private class NodeHeapComparator implements Comparator<Node> {
        public int compare(Node a, Node b) {
            if ((b.end - b.start) == (a.end - a.start)) {
                return a.id - b.id;
            }
            return (b.end - b.start) - (a.end - a.start);
        }
    }
    public List<List<Integer>> consistentHashing(int n) {
        // write your code here
        List<List<Integer>> result = new ArrayList<>();
        if (n < 1) {
            return result;
        } else if (n == 1) {
            result.add(Arrays.asList(0, 359, 1));
            return result;
        }
        PriorityQueue<Node> maxHeap = new PriorityQueue(11, new NodeHeapComparator());
        maxHeap.offer(new Node(0, 359, 1));
        for (int i = 2; i <= n; i++) {
            Node node = maxHeap.poll();
            int mid = (node.start + node.end) / 2;
            maxHeap.offer(new Node(node.start, mid, node.id));
            maxHeap.offer(new Node(mid + 1, node.end, i));
        }
        while (!maxHeap.isEmpty()) {
            Node node = maxHeap.poll();
            result.add(Arrays.asList(node.start, node.end, node.id));
        }
        return result;
    }
}
```
