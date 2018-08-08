##GFS Client
[lintcode](https://www.lintcode.com/problem/gfs-client/description?source=ladder)

##Description
	Implement a simple client for GFS (Google File System, a distributed file system), it provides the following methods:

	read(filename). Read the file with given filename from GFS.
	write(filename, content). Write a file with given filename & content to GFS.
	There are two private methods that already implemented in the base class:

	readChunk(filename, chunkIndex). Read a chunk from GFS.
	writeChunk(filename, chunkIndex, chunkData). Write a chunk to GFS.
	To simplify this question, we can assume that the chunk size is chunkSize bytes. (In a real world system, it is 64M).
	The GFS Client's job is splitting a file into multiple chunks (if need) and save to the remote GFS server.
	chunkSize will be given in the constructor. You need to call these two private methods to implement read & write methods.

##Example
	GFSClient(5)
	read("a.txt")
	>> null
	write("a.txt", "World")
	>> You don't need to return anything, but you need to call writeChunk("a.txt", 0, "World") to write a 5 bytes chunk to GFS.
	read("a.txt")
	>> "World"
	write("b.txt", "111112222233")
	>> You need to save "11111" at chink 0, "22222" at chunk 1, "33" at chunk 2.
	write("b.txt", "aaaaabbbbb")
	read("b.txt")
	>> "aaaaabbbbb"


##思路
- 储存file -> chunkindex的关系，读取都依靠这个关系
- 使用了一个自增的id，确保放进GFS的chunkIndex不会重复
- 其实更好的办法应该同时解决碎片化的问题
- 因为当重新写一个File的时候，是删除原来的关系，然后使用现在的自增ID，原来的chunkIndex就浪费了
- 所以可以使用一个queue来储存已经删除的chunkIndex，然后每次写新数据，先写到这些删除的chunkIndex上


```java
/* Definition of BaseGFSClient
 * class BaseGFSClient {
 *     private Map<String, String> chunk_list;
 *     public BaseGFSClient() {}
 *     public String readChunk(String filename, int chunkIndex) {
 *         // Read a chunk from GFS
 *     }
 *     public void writeChunk(String filename, int chunkIndex,
 *                            String content) {
 *         // Write a chunk to GFS
 *     }
 * }
 */


public class GFSClient extends BaseGFSClient {
    /*
    * @param chunkSize: An integer
    */
    Map<String, List<Integer>> fileChunk;
    int chunkIndex;
    public GFSClient(int chunkSize) {
        // do intialization if necessary
        fileChunk = new HashMap<String, List<Integer>>();
        chunkIndex = 0;
    }

    /*
     * @param filename: a file name
     * @return: conetent of the file given from GFS
     */
    public String read(String filename) {
        // write your code here
        StringBuilder sb = new StringBuilder();

        if (!fileChunk.containsKey(filename)) {
            return null;
        }

        List<Integer> chunks = fileChunk.get(filename);

        for (Integer i : chunks) {
            String chunkString = readChunk(filename, i);
            sb.append(chunkString);
        }

        return sb.toString();
    }

    /*
     * @param filename: a file name
     * @param content: a string
     * @return: nothing
     */
    public void write(String filename, String content) {
        // write your code here
        if (fileChunk.containsKey(filename)) {
            fileChunk.remove(filename);
        }
        List<Integer> chunks = new ArrayList<Integer>();
        for (int i = 0; i < content.length(); i = i + 5) {
            String chunkFile = new String("");;
            if (i + 5 >= content.length()) {
                chunkFile = new String(content.substring(i, content.length()));
            } else {
                chunkFile = new String(content.substring(i, i + 5));
            }
            writeChunk(filename, chunkIndex, chunkFile);
            chunks.add(chunkIndex++);
        }
        fileChunk.put(filename, chunks);

    }
}
```
