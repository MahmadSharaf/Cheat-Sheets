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
