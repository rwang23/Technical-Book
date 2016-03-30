##Database
3.primary key；join（四种）和index 原理和作用
4.简单的sql语句：从table中找出成绩第二好的学生姓名； group by

####Primary Key
A primary key is a key in a relational database that is unique for each record. It is a unique identifier, such as a driver license number, telephone number (including area code), or vehicle identification number (VIN). A relational database must always have one and only one primary key.

####Unique Key
a unique key is a set of zero, one, or more attributes. The value(s) of these attributes are required to be unique for each tuple (row) in a relation.

####Foreign Key
A foreign key is a column (or columns) that references a column (most often the primary key) of another table. The purpose of the foreign key is to ensure referential integrity of the data. In other words, only values that are supposed to appear in the database are permitted.

####Expalin database to a child
You know how you have to put your toys away when you're done playing,
if you just throw your toys away, next time you may hardily find them,
but if you put them in the toy shelf, you can find them easily the next time you want to play with them?

A database is like a shelf to put your toys away, except the toys are data instead.

Now, the database can always find the right data easily - whether it's "all the dinosaur toys" or "all the transformer toys," the computer can get everything out to play with very quickly, because it's in a database.

####NoSql database
- MongoDB
- CouchDB
- BigTable
- Cassandra
- Hbase

###MongoDB
- Mongodb is one of the most popular document based NoSQL database as it stores data in JSON like documents.
- MongoDB is written in c++
- Ease of scale-out: MongoDB is easy to scale
- Schema less : MongoDB is document database in which one collection holds different different documents. Number of fields, content and size of the document can be differ from one document to another.
- used for Big Data, User Data Management


###Relational vs No-relational
- SQL databases are primarily called as Relational Databases (RDBMS); whereas NoSQL database are primarily called as non-relational or distributed database.
- SQL databases are table based databases whereas NoSQL databases are document based, key-value pairs, graph databases or wide-column stores.
- SQL databases have predefined schema whereas NoSQL databases have dynamic schema for unstructured data
- SQL databases are vertically scalable whereas the NoSQL databases are horizontally scalable. SQL databases are scaled by increasing the horse-power of the hardware. NoSQL databases are scaled by increasing the databases servers in the pool of resources to reduce the load.
- SQL databases uses SQL ( structured query language ) for defining and manipulating the data, which is very powerful. In NoSQL database, queries are focused on collection of documents. Sometimes it is also called as UnQL (Unstructured Query Language). The syntax of using UnQL varies from database to database.
- SQL database examples: MySql, Oracle, Sqlite, Postgres and MS-SQL. NoSQL database examples: MongoDB, BigTable, Redis, RavenDb, Cassandra, Hbase, Neo4j and CouchDb
- For complex queries: SQL databases are good fit for the complex query intensive environment whereas NoSQL databases are not good fit for complex queries.
- For scalability: In most typical situations, SQL databases are vertically scalable. You can manage increasing load by increasing the CPU, RAM, SSD, etc, on a single server. On the other hand, NoSQL databases are horizontally scalable. You can just add few more servers easily in your NoSQL database infrastructure to handle the large traffic.

###SQL joins
- INNER JOIN: Returns only matched row when there is at least one match in BOTH tables
- LEFT JOIN: Return all rows from the left table, and the matched rows from the right table
- RIGHT JOIN: Return all rows from the right table, and the matched rows from the left table
- FULL JOIN: A FULL OUTER JOIN is a union of the LEFT OUTER JOIN and RIGHT OUTER JOIN.
- OUter join: combine two tables into one no matter they match or not

###SQL injection
inject” his harmful/malicious SQL code into someone else’s database, and force that database to run his SQL
####How to prevent
escaping strings
use Prepared Statements

###Database index
####How it does
[how it does](http://www.tutorialspoint.com/sql/sql-indexes.htm)
- Indexes are special lookup tables that the database search engine can use to speed up data retrieval. Simply put, an index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.
- For example, if you want to reference all pages in a book that discuss a certain topic, you first refer to the index, which lists all topics alphabetically and are then referred to one or more specific page numbers.
- Creating an index involves the CREATE INDEX statement, which allows you to name the index, to specify the table and which column or columns to index, and to indicate whether the index is in ascending or descending order.

####How it work
[how it work](http://stackoverflow.com/questions/1108/how-does-database-indexing-work)


###Clustered index
[Video](https://www.youtube.com/watch?v=ITcOiLSfVJQ)
A clustered index determines the order in which the rows of a table are stored on disk. If a table has a clustered index, then the rows of that table will be stored on disk in the same exact order as the clustered index.

Remember that an index is usually a tree data structure – and leaf nodes are the nodes that are at the very bottom of that tree. In other words, a clustered index basically contains the actual table level data in the index itself.

####Advantages
the query will run much faster than if the rows were being stored in some random order on the disk.

####Disadvantages
disadvantage to using a clustered index is the fact that if a given row has a value updated in one of it’s (clustered) indexed columns what typically happens is that the database will have to move the entire row so that the table will continue to be sorted in the same order as the clustered index column
