##Database
3.primary key；join（四种）和index 原理和作用
4.简单的sql语句：从table中找出成绩第二好的学生姓名； group by

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

###Database index
####How it does
[how it does](http://www.tutorialspoint.com/sql/sql-indexes.htm)
- Indexes are special lookup tables that the database search engine can use to speed up data retrieval. Simply put, an index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.
- For example, if you want to reference all pages in a book that discuss a certain topic, you first refer to the index, which lists all topics alphabetically and are then referred to one or more specific page numbers.
- Creating an index involves the CREATE INDEX statement, which allows you to name the index, to specify the table and which column or columns to index, and to indicate whether the index is in ascending or descending order.

####How it work
[how it work](http://stackoverflow.com/questions/1108/how-does-database-indexing-work)
