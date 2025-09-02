## Cassandra


`CREATE KEYSPACE mykeyspace WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 1 };` ## create a keyspace(analogous to a database in RDBMS)


`DESCRIBE KEYSPACES;` ## list keyspaces

`USE mykeyspace;` ## use keyspace mykeyspace

`DESCRIBE TABLES;` ## list tables in a keyspace

`DESCRIBE KEYSPACE mykeyspace;` ## list tables in keyspace mykeyspace

`SELECT * FROM mytable;`  ##List all rows and columns in table mytable

`DROP TABLE mytable;` ## drop table mytable

`DROP KEYSPACE mykeyspace;` ## drop keyspace mykeyspace

















