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

## Arithmetic Operators

- `=`: equal to
- `<`: less than
- `>`: greater than
- `<=`: less than or equal
- `>=`: greater than or equal
- `!=`: not equal to
- `<>`: not equal to

## Logical Operators

- `LIKE`: supports a simple form of text pattern-matching. Only pulls rows where column has 'me' within the text.

  ```sql
  WHERE Col LIKE '%me%'
  ```

- `IN`: Working with both numeric and text columns. Can check one, two or many column values for which we want to pull data, but all within the same query. A filter for only rows with column of 'Y' or 'N'

  ```sql
  WHERE Col IN ('Y', 'N')
  ```

- `NOT`: NOT LIKE or NOT IN, can grab all of the rows that do not meet a particular criteria.
- `AND`: Within a WHERE statement to consider more than one logical clause at a time.

  ```sql
  WHERE column >= 6 AND column <= 10
  ```

- `BETWEEN`: when the same column is being used for different parts of AND statement. The results include the values of the endpoints. You will notice that using BETWEEN is tricky for dates! While BETWEEN is generally inclusive of endpoints, it assumes the time is at 00:00:00 (i.e. midnight) for dates. This is the reason why we set the right-side endpoint of the period at '2017-01-01'.

  ```sql
  WHERE column BETWEEN 6 AND 10
  WHERE occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
  ```

- `OR`: Can combine multiple statements.

## SQL Statements

- A piece correctly written SQL code.
- A way to manipulate data stored in a database.
- A Sentence.
- A way to read data in database.

## Formatting Best Practices

- SQL is case-sensitive in regard to this text data.
- Avoid Spaces in Table and Variable Names
- SQL queries ignore spaces
- Depending on your SQL environment, your query may need a semicolon at the end to execute.

## SQL clauses

- **WHERE**  
  The where clause expresses restrictions on the source tables — filtering a table for rows that follow a particular rule. where supports equalities, inequalities, and boolean operators (among other things). **WHERE** appears after the **FROM**, **JOIN**, and **ON** clauses, but before **GROUP BY**.

- **HAVING**  
  HAVING is the “clean” way to filter a query that has been aggregated, but this is also commonly done using a subquery. Essentially, any time you want to perform a **WHERE** on an element of your query that was created by an aggregate, you need to use **HAVING** instead. **HAVING** appears after the **GROUP BY** clause, but before the **ORDER BY** clause.

- **LIMIT** _count_:  
  Return just the first count rows of the result table.

- **LIMIT** _count_ **OFFSET** skip:  
  Return count rows starting after the first skip rows.

- **ORDER BY** _columns_
- **order by** _columns_ **desc**  
  Sort the rows using the columns (one or more, separated by commas) as the sort key. Numerical columns will be sorted in numerical order; string columns in alphabetical order. With **desc**, the order is reversed (desc-ending order).

- **GROUP BY** _columns_  
  Change the behavior of aggregations such as **MAX**, **COUNT**, and **SUN**. With **GROUP BY**, the aggregation will return one row for each distinct value in columns. Any column in the **SELECT** statement that is not within an aggregator must be in the **GROUP BY** clause.The **GROUP BY** always goes between **WHERE** and **ORDER BY**. You can **GROUP BY** multiple columns at once. The order of columns listed in the **ORDER BY** clause does make a difference. You are ordering the columns from left to right.

  *As with **ORDER BY**, you can substitute numbers for column names in the **GROUP BY** clause. It’s generally recommended to do this only when you’re grouping many columns, or if something else is causing the text in the **GROUP BY** clause to be excessively long.*

  *SQL evaluates the aggregations before the **LIMIT** clause. If you don’t **group by** any columns, you’ll get a 1-row result—no problem there. If you **group by** a column with enough unique values that it exceeds the **LIMIT** number, the aggregates will be calculated, and then some rows will simply be omitted from the results.*

- **DISTINCT**:  
  DISTINCT is always used in SELECT statements, and it provides the unique rows for all columns written in the SELECT statement. Therefore, you only use DISTINCT once in any particular SELECT statement.

  ```sql
  SELECT DISTINCT column1, column2, column3
  FROM table1;

  --xx SELECT DISTINCT column1, DISTINCT column2, DISTINCT column3
  ```
  
  *It’s worth noting that using DISTINCT, particularly in aggregations, can slow your queries down quite a bit.*

- **INSERT**:  
  The basic syntax for the insert statement:

  ```sql
  insert into * table ( column1, column2, … ) values (  val1, val2, … );
  ```

  - If the values are in the same order as the table's columns (starting with the first column), you don't have to specify the columns in the insert statement:  
    **insert into** _table values ( val1, val2, … );_
  - For instance, if a table has three columns (a, b, c) and you want to **insert into** a and b, you can leave off the column names from the insert statement. But if you want to insert into b and c, or a and c, you have to specify the columns.

### Date and time functions

- **DATE_TRUNC**:  
  allows you to truncate your date to a particular part of your date-time column. Common truncations are **day**, **month**, and **year**. Here is a great [blog](https://blog.modeanalytics.com/date-trunc-sql-timestamp-function-count-on/) post by Mode Analytics on the power of this function.
- **DATE_PART**:  
  can be useful for pulling a specific portion of a date, but notice pulling **month** or day of the week (**dow**) means that you are no longer keeping the years in order. Rather you are grouping for certain components regardless of which year they belonged in.

  *For additional functions you can use with dates, check out the documentation [here](https://www.postgresql.org/docs/9.1/static/functions-datetime.html), but the DATE_TRUNC and DATE_PART functions definitely give you a great start!*

  *You can reference the columns in your select statement in GROUP BY and ORDER BY clauses with numbers that follow the order they appear in the select statement.*

  ```sql
  SELECT standard_qty, DATE_TRUNC('year',occurred_at)

  FROM orders

  GROUP BY 1
  --(this 1 refers to standard_qty since it is the first of the columns included in the select statement)

  ORDER BY 1
  --(this 1 refers to standard_qty since it is the first of the columns included in the select statement)
  ```

- **DATE_TO**:  
  `DATE_PART('month', TO_DATE(month, 'month'))` here changed a month name into the number associated with that particular month.

### CASE statements

- The CASE statement always goes in the SELECT clause.
- CASE must include the following components: WHEN, THEN, and END. ELSE is an optional component to catch cases that didn’t meet any of the other previous CASE conditions.
- You can make any conditional statement using any conditional operator (like **WHERE**) between WHEN and THEN. This includes stringing together multiple conditional statements using AND and OR.
- You can include multiple WHEN statements, as well as an ELSE statement again, to deal with any unaddressed conditions.

  ```sql
  SELECT s.name, COUNT(*), SUM(o.total_amt_usd) total_spent,
       CASE WHEN COUNT(*) > 200 OR SUM(o.total_amt_usd) > 750000  THEN 'top'
       WHEN COUNT(*) > 150 OR SUM(o.total_amt_usd) > 500000 THEN  'middle'
       ELSE 'low' END AS sales_rep_level
  FROM orders o
  JOIN accounts a
  ON o.account_id = a.id
  JOIN sales_reps s
  ON s.id = a.sales_rep_id
  GROUP BY s.name
  ORDER BY 3 DESC;
  ```

### Database manipulation

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
    CREATE TABLE [table] ( [column] [type] [restriction] , … )  [rowrestriction] ;
    ```

  - Declaring a primary key: are unique for every row in a table. These are generally the first column in our database

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

  - Declaring relationships/foreign key: are the _primary key_ appearing in another table, which allows the rows to be non-unique.

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

### JOINS

The whole purpose of JOIN statements is to allow us to pull data from more than one table at a time.

1. **JOIN**: an INNER JOIN that only pulls data that exists in both tables.

   ```sql
   SELECT orders.*
   FROM orders
   JOIN accounts
   ON orders.account_id = accounts.id;
   ```

2. **LEFT JOIN**: an **LEFT OUTER JOIN** that pulls all the data that exists in both tables, as well as all of the rows from the table in the FROM even if they do not exist in the JOIN statement.
3. **RIGHT JOIN**: an **RIGHT OUTER JOIN** that pulls all the data that exists in both tables, as well as all of the rows from the table in the JOIN even if they do not exist in the FROM statement.

   ```SQL
   SELECT *
   FROM left table
   LEFT/RIGHT JOIN right table
   ```

4. **OUTER JOIN**: This will return the inner join result set, as well as any unmatched rows from either of the two tables being joined.

#### Pro Tip

When the database executes the JOIN and everything in the ON clause first. Think of this as building the new result set. That result set is then filtered using the WHERE clause.

## Alias

You learned that you can alias tables and columns using AS or not using it. This allows you to be more efficient in the number of characters you need to write, while at the same time you can assure that your column headings are informative of the data in your table.

## Nulls

- NULLs are different than a zero - they are cells where data does not exist.
- When identifying NULLs in a WHERE clause, we write IS NULL or IS NOT NULL. We don't use `=`, because NULL isn't considered a value in SQL. Rather, it is a property of the data.
- NULLs frequently occur when performing a LEFT or RIGHT JOIN. when some rows in the left table of a left join are not matched with rows in the right table, those rows will contain some NULL values in the result set.
- NULLs can also occur from simply missing data in our database.
- We can COALESCE to substitute NULL with values. `COALESCE(column, 'value')`

## Aggregators

- **COUNT**: the Number of Rows in a Table. COUNT does not consider rows that have NULL values.
- **SUM**: can only use SUM on numeric columns.
- **MIN** & **MAX** : are similar to COUNT in that they can be used on non-numerical columns and ignore NULL values. Depending on the column type, MIN will return the lowest number, earliest date, or non-numerical value as early in the alphabet as possible. MAX does the opposite.
- **AVG**: returns the mean of the data. This aggregate function again ignores the NULL values in both the numerator and the denominator. If you want to count NULLs as zero, you will need to use SUM and COUNT. However, this is probably not a good idea if the NULL values truly just represent unknown values for a cell.

## Subquery

- It is a method for being able to write a query that creates a table, and then write a query that interacts with this newly created table. Sometimes the question you are trying to answer doesn't have an answer when working directly with existing tables in database.

  ```sql
  SELECT *
  FROM (SELECT DATE_TRUNC('day',occurred_at) AS day,
             channel, COUNT(*) as events
       FROM web_events
       GROUP BY 1,2
       ORDER BY 3 DESC) sub;
  ```

- In the first subquery you wrote, you created a table that you could then query again in the **FROM** statement. However, if you are only returning a single value, you might use that value in a logical statement like **WHERE**, **HAVING**, or even **SELECT** - the value could be nested within a **CASE** statement.

- Note that you should not include an alias when you write a subquery in a conditional statement. This is because the subquery is treated as an individual value (or set of values in the **IN** case) rather than as a table. Also, notice the query here compared a single value. If we returned an entire column **IN** would need to be used to perform a logical argument. If we are returning an entire table, then we must use an ALIAS for the table, and perform additional logic on the entire table

### Subquery Formatting

- The important thing to remember when using subqueries is to provide some way for the reader to easily determine which parts of the query will be executed together. Most people do this by indenting the subquery in some way - you saw this with the solution blocks in the previous concept. Additionally, if we have a GROUP BY, ORDER BY, WHERE, HAVING, or any other statement following our subquery, we would then indent it at the same level as our outer query.

- The query below is applying additional statements to the outer query, so you can see there are GROUP BY and ORDER BY statements used on the output are not tabbed. The inner query GROUP BY and ORDER BY statements are indented to match the inner table.

  ```sql
  SELECT *
  FROM (SELECT DATE_TRUNC('day',occurred_at) AS day,
                  channel, COUNT(*) as events
        FROM web_events
        GROUP BY 1,2
        ORDER BY 3 DESC) sub
  GROUP BY day, channel, events
  ORDER BY 2 DESC;
  ```

### WITH statement or Common Table Expression (CTE)

- The **WITH** statement is often called a Common Table Expression or CTE. Though these expressions serve the exact same purpose as subqueries, they are more common in practice, as they tend to be cleaner for a future reader to follow the logic.

  ```sql
  WITH table1 AS (
            SELECT *
            FROM web_events),

       table2 AS (
            SELECT *
            FROM accounts)


  SELECT *
  FROM table1
  JOIN table2
  ON table1.account_id = table2.id;
  ```

## Data Cleaning

- **LEFT**:  
  LEFT pulls a specified number of characters for each row in a specified column starting at the beginning (or from the left). As you saw here, you can pull the first three digits of a phone number using `LEFT(phone_number, 3)`.

- **RIGHT**:  
  pulls a specified number of characters for each row in a specified column starting at the end (or from the right). As you saw here, you can pull the last eight digits of a phone number using `RIGHT(phone_number, 8).`

- **LENGTH**:  
  provides the number of characters for each row of a specified column. Here, you saw that we could use this to get the length of each phone number as `LENGTH(phone_number)`.

- **TRIM**:
  it can be used to remove characters from the beginning and end of a string. This can remove unwanted spaces at the beginning or end of a row that often happen with data being moved from Excel or other storage systems.

- **POSITION**:  
  takes a character and a column, and provides the index where that character is for each row. The index of the first position is 1 in SQL. If you come from another programming language, many begin indexing at 0. Here, you saw that you can pull the index of a comma as `POSITION(',' IN city_state)`.

- **STRPOS**:  
  provides the same result as POSITION, but the syntax for achieving those results is a bit different as shown here: `STRPOS(city_state, ',')`.

- **LOWER** or **UPPER**:  
  to make all of the characters lower or uppercase.

- **CONCAT** or **Piping `||`**:  
  Each of these will allow you to combine columns together across rows. You see how first and last names stored in separate columns could be combined together to create a full name: `CONCAT(first_name, ' ', last_name)` or with piping as `first_name || ' ' || last_name`.

- **CAST** or **`::`**:  
  **CAST** is actually useful to change lots of column types. Commonly you might be doing as you saw here, where you change a string to a date using `CAST(date_column AS DATE)` or `date_column::DATE`. However, you might want to make other changes to your columns in terms of their data types. You can see other examples [here](http://www.postgresqltutorial.com/postgresql-cast/).


Most of the functions presented in this lesson are specific to strings. They won’t work with dates, integers or floating-point numbers. However, using any of these functions will automatically change the data to the appropriate type.

There are a number of variations of these functions, as well as several other string functions not covered here. Different databases use subtle variations on these functions, so be sure to look up the appropriate database’s syntax if you’re connected to a private database.The [Postgres literature](http://www.postgresql.org/docs/9.1/static/functions-string.html) contains a lot of the related functions.

## Rules for normalized tables

When creating a database, it is really important to think about how data will be stored. This is known as normalization, and it is a huge part of most SQL classes.

1. **Every row has the same number of columns.** or  
   **Are the tables storing logical groupings of the data?**  
    In practice, the database system won't let us literally have different numbers of columns in different rows. But if we have columns that are sometimes empty (null) and sometimes not, or if we stuff multiple values into a single field, we're bending this rule.

2. **There is a unique key and everything in a row says something about the key.**  
   The key may be one column or more than one. It may even be the whole row. But we don't have duplicate rows in a table.

   More importantly, if we are storing non-unique facts — such as people's names — we distinguish them using a unique identifier such as a serial number. This makes sure that we don't combine two people's grades or parking tickets just because they have the same name.

3. **Facts that don't relate to the key belong in different tables.**  
   The example here was the `items` table, which had items, their locations, and the location's street addresses in it. The address isn't a fact about the item; it's a fact about the location. Moving it to a separate table saves space and reduces ambiguity, and we can always reconstitute the original table using a join.

4. **Tables shouldn't imply relationships that don't exist.**  
   The example here was the `job_skills` table, where a single row listed one of a person's technology skills (like 'Linux') and one of their language skills (like 'French'). This made it look like their Linux knowledge was specific to French, or vice versa … when that isn't the case in the real world. Normalizing this involved splitting the tech skills and job skills into separate tables.

### References

1. William Kent's paper ["A Simple Guide to Five Normal Forms in Relational Database Theory"](http://www.bkent.net/Doc/simple5.htm) for a lot more about normalization and how it can help your database design.
2. [Wikipedia's article](http://en.wikipedia.org/wiki/Database_normalization) on database normalization is somewhat brief, but describes some of the history of normalization as well as some more of the motivations for it.
3. Detailed info about [normalization](https://www.itprotoday.com/sql-server/sql-design-why-you-need-database-normalization)
4. You will sometimes hear about denormalization as an approach to making database queries faster by avoiding joins. On modern database systems (such as PostgreSQL) it is often possible to meet the same goals using tools such as [indexes](http://www.postgresql.org/docs/9.4/static/sql-createindex.html) and [materialized views](http://www.postgresql.org/docs/9.4/static/sql-creatematerializedview.html).
