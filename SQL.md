#SQL: General

## Basics

Data types
  Text: any alphanumeric characters
  Integer: whole numbers
  Real: numbers with decimals
  Blob: binary data
General commands
  List all tables in database: .tables
  Look at structure of database: .schema
  Exit SQLite: .quit
  Output name of each column: .header on
  Enter column mode: .mode column
    Adjust and normalize column width: .width auto
    Customize column width: .width NUM1, NUM2
  Access column by table name and column name: table_name.column_name
Command line
  Execute file: sqlite3 database_name.db < file_name.sql  

## Making Databases and Tables

Databases
  Create: sqlite3 database_name.db
  Delete: outside of sqlite3, rm database_name.db
Tables
  Create: CREATE TABLE table_name( <br> id INTEGER PRIMARY KEY, <br> column_name DATA_TYPE, <br> column_name DATA_TYPE <br> );
    Default primary key in SQLite: row_id
    Required value: NOT NULL
    Must be unique: UNIQUE
  Delete: DROP TABLE table_name;
  Add column: ALTER TABLE table_name ADD COLUMN column_name DATA_TYPE;

## Queries

Inserting
  Insert: INSERT INTO table_name (column_name, column_name) VALUES (value, value), (value, value);
  Placeholder for missing values: NULL
Selecting
  Columns by name: SELECT column_name, column_name FROM table_name;
  All columns: SELECT * FROM table_name;
  Unique values: SELECT DISTINCT column_name FROM table_name;
  Aliasing the return value: SELECT column_name AS new_column_name FROM table_name;
Basic queries (append to select)
  Choose results between range: BETWEEN number AND number
  Conditionals: WHERE conditional
    Null value: WHERE column_name IS NULL
  Limit number of results: LIMIT number
  Look for a string within a string: LIKE '%string%'
  Connect queries: AND or OR
Aggregate functions
  Define: SELECT function FROM table_name;
  Average: AVG(column_name)
  Sum: SUM(column_name)
  Count: COUNT(column_name)
  Minimum: MIN(column_name)
  Maximum: MAX(column_name)
Grouping and sorting
  Order results by column: ORDER BY column_name ASC|DESC, column_name ASC|DESC;
    Defaults to ascending
  Group results by value in column: GROUP BY column_name;
  Aggregates: HAVING function;
Updating
  Update values: UPDATE table_name SET column_name = new_value WHERE column_name = value;
  Delete row: DELETE FROM table_name WHERE column_name = value;

## Table Relations

Joins
  Def: SELECT table_name.column_name FROM table_a TYPE JOIN table_b ON table_b.foreign_key_column = table_a.foreign_key_column
Types (SQLite compatible)
  INNER: all rows where there is a match
  LEFT: all rows from left, and rows where there is a match
Types (not SQLite compatible)
  RIGHT: all rows from right, and rows where there is a match
  FULL: all rows when there is a match in ONE of the tables
Join tables
  Create table: CREATE TABLE table_a_table_b ( <br> a_id INTEGER, <br> b_id INTEGER <br> );
  Insert data: INSERT INTO a_b (a_id, b_id) VALUES (value, value)
  Using the table: SELECT table_a.column_name FROM table_a INNER JOIN table_a_table_b ON table_b.b_id = table_a_table_b.b_id
