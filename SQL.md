# SQL Cheat Sheet

## SQL Types

### Text and Strings

- **varchar(MAX)** — a string of any length, like Python str or unicode types.
- **char(n)** — a string of exactly n characters.
- **varchar(n)** — a string of up to n characters.

### Numeric types

- **integer** — an integer value, like Python **int**.
- **real** — a floating-point value, like Python **float**. Accurate up to six decimal places.
- **double precision** — a higher-precision floating-point value. Accurate up to 15 decimal places.
- **decimal** — an exact decimal value.

### Date and time types

- **date** — a calendar date; including year, month, and day.
- **time** — a time of day.
- **timestamp** — a date and time together.

### Resources

- <https://www.postgresql.org/docs/9.4/datatype.html>

## Comparison Operators

- `=`: equal to
- `<`: less than
- `>`: greater than
- `<=`: less than or equal
- `>=`: greater than or equal
- `!=`: not equal to
- `LIKE`: supports a simple form of text pattern-matching

## SQL Elements

- **where**  
  The where clause expresses restrictions on the source tables — filtering a table for rows that follow a particular rule. where supports equalities, inequalities, and boolean operators (among other things

- **HAVING**  
  The having clause expresses restrictions on the results..after aggregation

- **limit** _count_:  
  Return just the first count rows of the result table.

- **limit** _count_ **offset** :  
  Return count rows starting after the first skip rows.

- **order by** _columns_
- **order by** _columns_ **desc**  
  Sort the rows using the columns (one or more, separated by commas) as the sort key. Numerical columns will be sorted in numerical order; string columns in alphabetical order. With desc, the order is reversed (desc-ending order).

- **group by** _columns_  
  Change the behavior of aggregations such as **max**, **count**, and **sum**. With **group by**, the aggregation will return one row for each distinct value in columns.

- **INSERT**:  
  The basic syntax for the insert statement:

  ```sql
  insert into * table ( column1, column2, … ) values (  val1, val2, … );
  ```

  - If the values are in the same order as the table's columns (starting with the first column), you don't have to specify the columns in the insert statement:  
    **insert into** _table values ( val1, val2, … );_
  - For instance, if a table has three columns (a, b, c) and you want to **insert into** a and b, you can leave off the column names from the insert statement. But if you want to insert into b and c, or a and c, you have to specify the columns.

- **UPDATE**:  
  It updates the table fields

  - The syntax of the update statement:

  ```sql
  UPDATE [table] SET [column] = [value] WHERE [restriction] ;
  ```

  - The restriction works the same as in select and supports the same set of operators on column values.

- **DELETE**:  
  It deletes records from the table

  - The syntax of the DELETE statement:

  ```sql
  DELETE FROM [table] WHERE [restriction] ;
  ```

  - The restriction works the same way as in select, with the same set of operators allowed.

- **CREATE DATABASE**  
  Create a new database

  - The syntax of the CREATE DATABASE statement:

  ```sql
  CREATE DATABASE [database_name]
  ```

- **DROP DATABASE**  
  This deletes/removes the database

  - The syntax of the DROP DATABASE statement:

  ```sql
  DROP DATABASE [database_name]
  ```

- **CREATE TABLE**  
  This Creates a new table in the database

  - The syntax of the CREATE TABLE statement:

  ```sql
  CREATE TABLE [table] ( [column] [type] [restriction] , … ) [rowrestriction] ;
  ```

  - Declaring a primary key:

  ```sql
  CREATE TABLE [table_name] (
    [column_name] [column_type] PRIMARY KEY,
    ..);
  ```

  Or for multi-column Primary KEY

  ```sql
  CREATE TABLE [table_name] (
    [column1_name] [column1_type],
    [column2_name] [column2_type]
    ..,
    PRIMARY KEY ([column1_name],[column2_name])
    );
  ```

  - Declaring relationships/foreign key

  ```sql
  CREATE TABLE [table_name] (
    [column_name] [column_type] REFERENCE [referenced_table] (state_column_name_if_different),
    ...
  );
  ```

- **DROP TABLE**  
  This deletes/removes a table from the database

  - The syntax of the DROP TABLE statement:

  ```sql
  DROP TABLE [table_name] ;
  ```

- **CREATE VIEW**  
  It is a select query stored in the database that can be used as a table

  ```sql
  CREATE VIEW [view_name] AS
  SELECT [column_name], ..
  FROM [table_name]
  ```

## Rules for normalized tables

1. **Every row has the same number of columns.**  
   In practice, the database system won't let us literally have different numbers of columns in different rows. But if we have columns that are sometimes empty (null) and sometimes not, or if we stuff multiple values into a single field, we're bending this rule.

1. **There is a unique key and everything in a row says something about the key.**  
   The key may be one column or more than one. It may even be the whole row. But we don't have duplicate rows in a table.

   More importantly, if we are storing non-unique facts — such as people's names — we distinguish them using a unique identifier such as a serial number. This makes sure that we don't combine two people's grades or parking tickets just because they have the same name.

1. **Facts that don't relate to the key belong in different tables.**  
   The example here was the `items` table, which had items, their locations, and the location's street addresses in it. The address isn't a fact about the item; it's a fact about the location. Moving it to a separate table saves space and reduces ambiguity, and we can always reconstitute the original table using a join.

1. **Tables shouldn't imply relationships that don't exist.**  
   The example here was the `job_skills` table, where a single row listed one of a person's technology skills (like 'Linux') and one of their language skills (like 'French'). This made it look like their Linux knowledge was specific to French, or vice versa … when that isn't the case in the real world. Normalizing this involved splitting the tech skills and job skills into separate tables.

### References

1. William Kent's paper ["A Simple Guide to Five Normal Forms in Relational Database Theory"](http://www.bkent.net/Doc/simple5.htm) for a lot more about normalization and how it can help your database design.
2. [Wikipedia's article](http://en.wikipedia.org/wiki/Database_normalization) on database normalization is somewhat brief, but describes some of the history of normalization as well as some more of the motivations for it.
3. You will sometimes hear about denormalization as an approach to making database queries faster by avoiding joins. On modern database systems (such as PostgreSQL) it is often possible to meet the same goals using tools such as [indexes](http://www.postgresql.org/docs/9.4/static/sql-createindex.html) and [materialized views](http://www.postgresql.org/docs/9.4/static/sql-creatematerializedview.html).
