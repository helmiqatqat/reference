# Select Statement

To retrieve data from a SQL database, we need to write SELECT statements, which are often colloquially refered to as queries. A query in itself is just a statement which declares what data we are looking for, where to find it in the database, and optionally, how to transform it before it is returned.

## Select query for a specific columns

the most basic query we could write would be one that selects for a couple columns (properties) of the table with all the rows (instances).

```sql
SELECT column, another_column, …
FROM mytable;
```

The result of this query will be a two-dimensional set of rows and columns, effectively a copy of the table, but only with the columns that we requested.

## Select query for all columns

If we want to retrieve absolutely all the columns of data from a table, we can then use the asterisk (*) shorthand in place of listing all the column names individually.

```sql
SELECT * FROM mytable;
```

This query, in particular, is really useful because it's a simple way to inspect a table by dumping all the data at once.
