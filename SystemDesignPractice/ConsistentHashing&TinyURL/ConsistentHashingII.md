##Consistent Hashing II
[Lintcode](https://www.lintcode.com/problem/consistent-hashing-ii/description)

####Description

	在 Consistent Hashing I 中我们介绍了一个比较简单的一致性哈希算法，这个简单的版本有两个缺陷：

	增加一台机器之后，数据全部从其中一台机器过来，这一台机器的读负载过大，对正常的服务会造成影响。

	当增加到3台机器的时候，每台服务器的负载量不均衡，为1:1:2。
	为了解决这个问题，引入了 micro-shards 的概念，一个更好的算法是这样：

	将 360° 的区间分得更细。从 0~359 变为一个 0 ~ n-1 的区间，将这个区间首尾相接，连成一个圆。

	当加入一台新的机器的时候，随机选择在圆周中撒 k 个点，代表这台机器的 k 个 micro-shards。

	每个数据在圆周上也对应一个点，这个点通过一个 hash function 来计算。

	一个数据该属于那台机器负责管理，是按照该数据对应的圆周上的点在圆上顺时针碰到的第一个 micro-shard 点所属的机器来决定。
	n 和 k在真实的 NoSQL 数据库中一般是 2^64 和 1000。

	请实现这种引入了 micro-shard 的 consistent hashing 的方法。主要实现如下的三个函数：

	create(int n, int k)
	addMachine(int machine_id) // add a new machine, return a list of shard ids.
	getMachineIdByHashCode(int hashcode) // return machine id

####Node
	create(100, 3)
	addMachine(1)
	>> [3, 41, 90]  => 三个随机数
	getMachineIdByHashCode(4)
	>> 1
	addMachine(2)
	>> [11, 55, 83]
	getMachineIdByHashCode(61)
	>> 2
	getMachineIdByHashCode(91)
	>> 1

####思路
- create 相当于是一个setup
- 建立一个random number -> machine ID 的Map
- addMachine的时候每次检查random number是不是已经生成过了(生成random number可以不直接全范围生成,只需要每次生成0-20,21-40这样,可以保证更好的均匀分布,不然random可能是89,90,91,92,都聚集在一起,就没什么意义了)
- 然后使用Binary search每次去查找machine
- 更好的办法是,使用treemap

```java
public class Solution {

    private static int machine_numbers;
    private static int shard_numbers;
    private static Map<Integer, Integer> shardsMap;
    private static List<Integer> shards;


    public Solution(int n, int k) {
        machine_numbers = n;
        shard_numbers = k;
        shardsMap = new HashMap<Integer, Integer>();
        shards = new ArrayList<Integer>();
    }
    /*
     * @param n: a positive integer
     * @param k: a positive integer
     * @return: a Solution object
     */
    public static Solution create(int n, int k) {
        // Write your code here
        return new Solution(n, k);
    }

    /*
     * @param machine_id: An integer
     * @return: a list of shard ids
     */
    public List<Integer> addMachine(int machine_id) {
        // write your code here
        List<Integer> list = new ArrayList<Integer>();

        for (int i = 1; i <= shard_numbers; i++) {
            Random r = new Random();
            int random = r.nextInt(machine_numbers);
            while (shardsMap.containsKey(random)) {
                random = r.nextInt(machine_numbers);
            }
            shardsMap.put(random, machine_id);
            list.add(random);
        }

        shards.addAll(list);
        Collections.sort(shards);

        return list;
    }

    /*
     * @param hashcode: An integer
     * @return: A machine id
     */
    public int getMachineIdByHashCode(int hashcode) {
        // write your code here
        if (shardsMap.containsKey(hashcode)) {
            return shardsMap.get(hashcode);
        }

        int shardID =  binarySearch(shards, hashcode);
        return shardsMap.get(shardID);
    }

    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(List<Integer> nums, int target) {
        //write your code here
        if (nums == null || nums.size() == 0) {
            return -1;
        }

        int end = nums.size() - 1;
        int start = 0;

        while (end > start + 1) {
            int mid = start + (end - start) / 2;
            if (nums.get(mid) == target) {
                start = mid;
            } else if(nums.get(mid) > target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        if (target > nums.get(end)) {
            end = 0;
        }
        return nums.get(end);
    }
}
```
