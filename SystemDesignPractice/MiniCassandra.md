##Mini Cassandra

	502. Mini Cassandra
	Cassandra is a NoSQL storage. The structure has two-level keys.

	Level 1: raw_key. The same as hash_key or shard_key.
	Level 2: column_key.
	Level 3: column_value
	raw_key is used to hash and can not support range query. let's simplify this to a string.
	column_key is sorted and support range query. let's simplify this to integer.
	column_value is a string. you can serialize any data into a string and store it in column value.

	implement the following methods:

	insert(raw_key, column_key, column_value)
	query(raw_key, column_start, column_end) // return a list of entries

####Note
	Example
	insert("google", 1, "haha")
	query("google", 0, 1)
	>> [（1, "haha")]

####Challenge

####Tags Expand
NoSQL

####思路一
-  使用HashMap和List, hashmap存rowKey指向list,list存Column(columnkey, value). 因为columnkey要求已经排序的,这样的话在存的时候需要每次对list进行依照columnkey大小进行sort
- 在取出的时候,因为需要范围取出,所以要对list进行遍历,取出所有满足olumn.key >= column_start && column.key <= column_end
- 写时间复杂度 O(nlogn) 读时间复杂度 O(n)

####思路二
- 使用HashMap和PriorityQueue,使用HashMap和PriorityQueue,PriorityQueu存Column(columnkey, value). 这样在取出的时候保证他们已经sort了,但是insert的时候时间复杂度是O(logn).
- 读的时候,不能直接遍历PriorityQueue, 要么就是遍历生成一个List,再sort一个list,但是这样时间就多了,要么就构造一个dummy PriorityQueue, 每次从它里边去读,这样只需要O(n)的时间
- 写时间复杂度O(logn),读时间复杂度 O(n)

####注意事项
- PriorityQueue只能保证每次出最大/最小值,直接遍历不会保证顺序,所以要合理利用dummy

####问题
- 题目中并未提及如一种情况:
- 我的结果中 [(3, "ODAMGH"),(3, "KELFJN"),(4, "EAKNIF"),(7, "DGFINL")]
- 理想结果是 [(3, "KELFJN"),(4, "EAKNIF"),(7, "DGFINL")]
- 说明如果出现了rowkey(唯一),但是columnkey不同,value相同的情况,那么将产生替换,如结果中,4替代了3,而不是在加上4

####初次代码

```java
/**
 * Definition of Column:
 * public class Column {
 *     public int key;
 *     public String value;
 *     public Column(int key, String value) {
 *         this.key = key;
 *         this.value = value;
 *    }
 * }
 */


public class MiniCassandra {

    Map<String, PriorityQueue<Column>> miniCassandra;

    static class ColumnSort implements Comparator<Column> {

        public int compare(Column c1, Column c2) {
            return c1.key - c2.key;
        }
    }

    public MiniCassandra() {
        // do intialization if necessary
        miniCassandra = new HashMap<String, PriorityQueue<Column>>();
    }

    /*
     * @param raw_key: a string
     * @param column_key: An integer
     * @param column_value: a string
     * @return: nothing
     */
    public void insert(String raw_key, int column_key, String column_value) {
        // write your code here
        PriorityQueue<Column> columns;
        Column column = new Column(column_key, column_value);

        ColumnSort sort = new ColumnSort();
        if (!miniCassandra.containsKey(raw_key)) {
            columns = new PriorityQueue<Column>(10, sort);
            columns.offer(column);
            miniCassandra.put(raw_key, columns);
        } else {
            columns = miniCassandra.get(raw_key);
            if (columns.contains(column_key)) {
                columns.remove(column_key);
            }
            columns.offer(column);
        }
    }

    /*
     * @param raw_key: a string
     * @param column_start: An integer
     * @param column_end: An integer
     * @return: a list of Columns
     */
    public List<Column> query(String raw_key, int column_start, int column_end) {
        // write your code here
        List<Column> results = new ArrayList<Column>();

        if (column_start > column_end) {
            return results;
        }

        if (!miniCassandra.containsKey(raw_key)) {
            return results;
        }

        PriorityQueue<Column> columns = miniCassandra.get(raw_key);
        List<Column> columnLists = pqtoList(columns);

        for (int i = 0; i < columnLists.size(); i++) {
            Column column = columnLists.get(i);
            if (column.key >= column_start && column.key <= column_end) {
                results.add(column);
            }
        }

        return results;

    }

    public List<Column> pqtoList(PriorityQueue<Column> columns) {

        List<Column> columnList = new ArrayList<Column>();
        PriorityQueue<Column> pqCopy = new PriorityQueue<Column>(columns);

        while(!pqCopy.isEmpty()){
            Column column = pqCopy.poll();
            columnList.add(column);
        }

        return columnList;
    }
}
```
