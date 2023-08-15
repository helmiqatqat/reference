# Multi-table queries with JOINs

Entity data in the real world is often broken down into pieces and stored across multiple orthogonal tables using a process known as **normalization**.

## Database Normalization

Database normalization is useful because it minimizes duplicate data in any single table, and allows for data in the database to grow independently of each other. As a trade-off, queries get slightly more complex since they have to be able to find data from different parts of the database, and performance issues can arise when working with many large tables.

## JOINs

Tables that share information about a single entity need to have a primary key that identifies that entity uniquely across the database. One common primary key type is an auto-incrementing integer (because they are space efficient), but it can also be a string, hashed value, so long as it is unique.

Using the **JOIN** clause in a query, we can combine row data across two separate tables using this unique key.

### INNER JOIN

The first of the joins is the **INNER JOIN**.

```sql
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

The INNER JOIN is a process that matches rows from the first table and the second table which have the same key (as defined by the ON constraint) to create a result row with the combined columns from both tables. After the tables are joined, the other clauses we learned previously are then applied.

So if we wrote the following SQL command,

```sql
SELECT * FROM mytable
INNER JOIN another_table;
```

What it basically does, joins each row in 'mytable' with a row in 'another_table'creating **n*m** total rows selected where **n** is the number of rows in 'mytable' and **m** is the number of rows in 'another_table'.

But if we specified the join as follows:

```sql
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id;
```

It will be eventually have **n** number of rows where **n** is number of rows in 'mytable'.

#### user_info_table

|id|username|password|
|--|--------|--------|
|1 |helmi   |1234    |
|2 |crow    |1234    |

#### user_image_table

|id|user_id |profile_image_link      |
|--|--------|------------------------|
|1 |2       |loremipsum.com/crow.jpg |
|2 |1       |loremipsum.com/helmi.jpg|

#### SQL Command

```sql
SELECT * FROM mytable
INNER JOIN another_table 
    ON id = another_table.id;
```

##### Resulting Table

|id|username|password|profile_image_link      |
|--|--------|--------|------------------------|
|1 |helmi   |1234    |loremipsum.com/helmi.jpg|
|2 |crow    |1234    |loremipsum.com/crow.jpg |

Depending on how you want to analyze the data, the INNER JOIN we used might not be sufficient because the resulting table only contains data that belongs in both of the tables.

### OUTER JOIN

If the two tables have asymmetric data, which can easily happen when data is entered in different stages, then we would have to use a LEFT JOIN, RIGHT JOIN or FULL JOIN instead to ensure that the data you need is not left out of the results.

```sql
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

Like the INNER JOIN these three new joins have to specify which column to join the data on.
When joining table A to table B, a LEFT JOIN simply includes rows from A regardless of whether a matching row is found in B. The RIGHT JOIN is the same, but reversed, keeping rows in B regardless of whether a match is found in A. Finally, a FULL JOIN simply means that rows from both tables are kept, regardless of whether a matching row exists in the other table.

When using any of these new joins, you will likely have to write additional logic to deal with NULLs in the result and constraints (more on this in the next lesson).

Like the INNER JOIN these three new joins have to specify which column to join the data on.
When joining table A to table B, a

1. **LEFT JOIN** simply includes rows from A regardless of whether a matching row is found in B.

2. The **RIGHT JOIN** is the same, but reversed, keeping rows in B regardless of whether a match is found in A.

3. Finally, a **FULL JOIN** simply means that rows from both tables are kept, regardless of whether a matching row exists in the other table.

**Important Note**: When using any of these new joins, you will likely have to write additional logic to deal with NULLs in the result and constraints (more on this in the next lesson).
