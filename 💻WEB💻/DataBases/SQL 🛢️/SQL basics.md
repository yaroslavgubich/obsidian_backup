Certainly! Below is a comprehensive #cheatsheet covering the #basics of #SQL, including data manipulation, querying, table creation, and modification commands. This cheatsheet is designed to provide you with a solid foundation for working with SQL databases.

### 1. **Data Query Language (DQL)**

- **SELECT**: Retrieve data from one or more tables.

```sql
SELECT column1, column2 FROM table_name;
SELECT * FROM table_name; -- '*' selects all columns
```

- **WHERE**: Specify conditions to filter records.

```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

- **ORDER BY**: Sort the result set.

```sql
SELECT column1, column2 FROM table_name ORDER BY column1 ASC|DESC;
```

- **GROUP BY**: Group rows sharing a property so aggregate functions can be applied to each group.

```sql
SELECT column, COUNT(*) FROM table_name GROUP BY column;
```

- **HAVING**: Filter groups by the result of aggregate functions.

```sql
SELECT column, COUNT(*) FROM table_name GROUP BY column HAVING COUNT(*) > 1;
```

- **JOIN**: Combine rows from two or more tables.

```sql
-- Inner join
SELECT columns FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name;

-- Left join
SELECT columns FROM table1 LEFT JOIN table2 ON table1.column_name = table2.column_name;

-- Right join
SELECT columns FROM table1 RIGHT JOIN table2 ON table1.column_name = table2.column_name;

-- Full outer join
SELECT columns FROM table1 FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
```

### 2. **Data Manipulation Language (DML)**

- **INSERT INTO**: Insert new records in a table.

```sql
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
```

- **UPDATE**: Modify existing records.

```sql
UPDATE table_name SET column1 = value1 WHERE condition;
```

- **DELETE**: Remove existing records.

```sql
DELETE FROM table_name WHERE condition;
```

### 3. **Data Definition Language (DDL)**

- **CREATE TABLE**: Create a new table.

```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ...
);
```

- **ALTER TABLE**: Modify an existing table (e.g., adding a column).

```sql
ALTER TABLE table_name ADD column_name datatype;
ALTER TABLE table_name DROP COLUMN column_name;
```

- **DROP TABLE**: Delete a table and its data.

```sql
DROP TABLE table_name;
```

### 4. **Constraints and Keys**

- **PRIMARY KEY**: Uniquely identifies each record.

```sql
CREATE TABLE table_name (
    ID int NOT NULL,
    column2 datatype,
    ...
    PRIMARY KEY (ID)
);
```

- **FOREIGN KEY**: Ensures referential integrity.

```sql
CREATE TABLE table_name (
    ID int,
    foreign_key_column datatype,
    ...
    FOREIGN KEY (foreign_key_column) REFERENCES other_table(other_table_column)
);
```

- **UNIQUE**: Ensures all values in a column are different.

```sql
CREATE TABLE table_name (
    column1 datatype UNIQUE,
    ...
);
```

- **NOT NULL**: Ensures a column cannot have a NULL value.

```sql
CREATE TABLE table_name (
    column1 datatype NOT NULL,
    ...
);
```

- **CHECK**: Ensures the value in a column meets a specific condition.

```sql
CREATE TABLE table_name (
    column1 datatype CHECK (condition),
    ...
);
```

### Conclusion

This cheatsheet covers the foundational aspects of SQL including data querying, manipulation, and definition, along with key constraints and table relationships. With these basics, you can perform a wide range of database operations, from simple queries to complex table manipulations. Experimenting with these commands in a real SQL environment will further solidify your understanding and proficiency in managing SQL databases.

https://www.codecademy.com/resources/docs/sql/commands
#cheatsheet #codecademy #cc #sql
How to SELECT  DISTINCT name FROM babies WHERE name LIKE 'S%' LIMIT 20;
![[Pasted image 20240313112444.png]]
#SQL #solutions

![[Pasted image 20240313114035.png]]
how to #order in #SQL 

how to #test #sql in #ruby 
![[Pasted image 20240313133702.png]]
![[Pasted image 20240313133801.png]]
**also : via extension: ctrl shift p and CREATE and RUN QUERY* 

![[Pasted image 20240313135616.png]]


#testing with #irb To test the given tasks in IRB (Interactive Ruby Shell) using the `sqlite3` gem, you first need to ensure that the `sqlite3` gem is installed in your Ruby environment. If it's not installed, you can install it by running `gem install sqlite3` in your terminal.

Once you have the `sqlite3` gem installed, you can test the provided code and the functions you need to implement. Here's a step-by-step guide on how to test each function in IRB:

### Step 1: Start IRB and Require sqlite3

Open your terminal and start IRB by simply typing `irb`, then load the `sqlite3` gem:

```ruby
require 'sqlite3'
```

### Step 2: Initialize Database Connection

Create a new database connection using the given code:

```ruby
db = SQLite3::Database.new("lib/db/jukebox.sqlite")
```

Make sure the path to the `jukebox.sqlite` database is correct and accessible from your current working directory.

### Step 3: Test Initial Code

Test the initial query to fetch and print rows from the `artists` table:

```ruby
rows = db.execute("SELECT * FROM artists LIMIT 3")
pp rows
```

run long line but nicely structured 

![[Pasted image 20240313141017.png]]
#find symbol or a word in a table and return the result 
![[Pasted image 20240313142314.png]] 
#SQL 
#solutions 
check for #empty #values #SQL #solutions 
![[Pasted image 20240313143134.png]]
#order #SQL #solutions 
![[Pasted image 20240313143706.png]]

#find #case sensitive letters in #SQL  
# [Can we match for a specific casing of text?](https://discuss.codecademy.com/t/can-we-match-for-a-specific-casing-of-text/379345)

![[Pasted image 20240313144610.png]]

#SQL  #count 
The `COUNT` function in SQL is used to return the number of items in a group. It's an aggregate function, meaning it summarizes multiple rows of data into a single result. Here are some examples to illustrate different uses of the `COUNT` function:

### 1. Counting All Rows in a Table
To count all rows in a table, regardless of null values or duplicates:

```sql
SELECT COUNT(*) FROM products;
```
This query returns the total number of rows in the `products` table.

### 2. Counting Non-Null Values in a Single Column
To count all non-null values in a specific column:

```sql
SELECT COUNT(column_name) FROM products;
```
If `column_name` is `price`, this query counts all rows where `price` is not null in the `products` table.

### 3. Counting Distinct Values
To count distinct values in a column (ignoring duplicates):

```sql
SELECT COUNT(DISTINCT column_name) FROM products;
```
Using `category` as `column_name`, this query counts the distinct categories in the `products` table, ignoring duplicate category entries.

### 4. Conditional Counts
To count rows that match a specific condition, you combine `COUNT` with a `WHERE` clause:

```sql
SELECT COUNT(*) FROM orders
WHERE order_date >= '2021-01-01';
```
This query counts orders placed on or after January 1, 2021.

### 5. Counting Within Groups
You can also use `COUNT` with the `GROUP BY` clause to count items within each group:

```sql
SELECT category, COUNT(*) AS total_products
FROM products
GROUP BY category;
```
This query counts the number of products in each category, grouping the results by category.

### 6. Count in a Join Operation
`COUNT` can be used in queries that involve joins to count related items across tables:

```sql
SELECT customers.customer_name, COUNT(orders.order_id) AS total_orders
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_name;
```
This query counts the number of orders for each customer by joining the `customers` and `orders` tables, grouping the results by customer name.

### Conclusion
The `COUNT` function is versatile and can be used in a variety of ways to aggregate data. Whether you're counting rows, distinct values, or conditional matches, `COUNT` provides valuable insights into the quantity of data matching your criteria.

how to #incert or #add a new column into an #SQL table 

``` sql
INSERT INTO celebs (id, name, age)  
VALUES (1, 'Justin Bieber', 29);
```

To #add an #empty column 

``` SQL 
ALTER TABLE celebs  
ADD COLUMN twitter_handle TEXT;
```

how to add #constrains #rules to #restrict user from entering wrong data in #sql? 
[_Constraints_](https://www.codecademy.com/resources/docs/sql/constraints?page_ref=catalog) that add information about how a column can be used are invoked after specifying the data type for a column. They can be used to tell the database to reject inserted data that does not adhere to a certain restriction. The statement below sets _constraints_ on the `celebs` table.
``` sql

CREATE TABLE celebs (  
   id INTEGER PRIMARY KEY,  
   name TEXT UNIQUE,  
   date_of_birth TEXT NOT NULL,  
   date_of_death TEXT DEFAULT 'Not Applicable'  
);
```
How to #specify #value #type for each row ?