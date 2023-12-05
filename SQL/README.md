# SQL BASICS

From SQLZOO, we can learn the basics of performing SQL queries.

Here is the **[website](https://].net/wiki/SQL_Tutorial)** to review the exercises.
Here are my **[solutions](https://github.com/bautret/Tutorials/tree/main/SQL/SQLZOO)** *(I'd recommend to try by yourself first)*.

Another great ressource to train is [SQLBOT](https://sqlbolt.com/).

### What you will find on this page

| FUNCTIONS                   |
| ----------------------------|
| SELECT                      |
| FROM                        |
| WHERE                       |
| IN                          |
| AS                          |
| LIKE %                      |
| AND ; OR ; NOT              |
| BETWEEN AND                 |
| ORDER BY ASC/DESC           |  
| SUM ; COUNT                 |
| DISTINCT                    |
| LIMIT                       |
| CASE WHEN ELSE END          |
| NULL                        |
| JOIN (LEFT ; RIGHT ; INNER) |

## SELECT

```sql
SELECT *
FROM table
```

1. You always want to start a **SQL QUERY** with **SELECT** *(the symbol * means **ALL**).*
2. You need to get the data from a **TABLE**.

```sql
SELECT column_1,
  column_2
FROM table
```

You don't have to select everything. You can choose specific columns. Each column is separated by a **comma**, except the last one. 

You don't have to go to the following line for each new element. However, it adds to readability.

```sql
SELECT column_1, 
  column_2
FROM table
WHERE name = xxx
```

You can filter the data by using **WHERE** and add the sign **=**
- If it is a string, use brackets (e.g.: WHERE country = 'France').
- If it is an integer, you don't need to use brackets (e.g.: WHERE year = 1995).

```sql
WHERE name IN ('Sweden', 'Norway', 'Denmark')
```

When you want to filter with several **INPUTS**, you use **IN** followed by parentheses and a comma to differentiate each element.

```sql
WHERE number >= 2000
```
|Signs          | What for              |
| ------------- | --------------------- |
| >             | Greater than          |
| >=            | Greater than or equal |
| <             | Less than             |
| >=            | Less than or equal    |

```sql
SELECT name,
  population/1000000
FROM world
```
You can **divide** or **multiply** a column by a number (if the column is containing integers).

```sql
SELECT name,
  GDP/population AS GDP_per_capita
FROM world
```
- You can **divide** or **multiply** a column by another column.
- You can rename a column by using **AS** and then the **new_name**.

```sql
SELECT name,
FROM world
WHERE name LIKE '%United%'
```
If you want to include part of a string in your filter, you can use **%**.

|% position     | What for                                 |
| ------------- | -----------------------------------------|
| %text%        | Look if the string contains the input    |
| %text         | Look if the string starts with the input |
| text%         | Look if the string ends with the input   |

```sql
SELECT name,
  area
FROM world
WHERE area > 3000000 OR population > 250000000
```
You can use operators in your filter (WHERE).

|OPERATOR       | What for                                      |
| ------------- | --------------------------------------------- |
| AND           | Need an addition of two or more elements      |
| OR            | Filter works with one or the other element(s) |     
| NOT           | Exclude certain element(s)                    |

```sql
SELECT name,
  population,
  area
FROM world
WHERE (area > 30000000 & population > 25000000) &
      (area < 30000000 & population < 25000000)
```
You can use **several operators** together.

```sql
WHERE year BETWEEN 2000 AND 2005
```
To specify a **range** (of dates, quantity etc.) you can use **BETWEEN** number_1 **AND** number_2.

```sql
SELECT name,
  year
FROM movie
ORDER BY year DESC
```
You can order the results in **ascending** (defaultor type **ASC**) and **descending** order (type **DESC**).

```sql
ORDER BY year DESC,
  name
```
You can add several ordering levels by adding other columns (for name, it will be ordered by ascending alphabetical order).

It is essential to have in mind the orders of execution.

|ORDER | CLAUSE   |
| -----| ---------|
| 1    | FROM     | 
| 2    | WHERE    |     
| 3    | GROUP BY |
| 4    | HAVING   |
| 5    | SELECT   |
| 6    | ORDER BY |
| 7    | LIMIT    |

```sql
ORDER BY subject IN ('economics','medicine'), subject,winner 
  name
```
You can set a particular value from a column as **last**. In this case, it will sort results by subject first, then winner **BUT** economics **then** medicine as **last**.

```sql
SELECT continent, MIN(name) AS name
FROM world
```
You can select the **MIN** or **MAX** value. *In the case of a string, it will use alphabetical orders; in the case of an integer, the minimum/maximum numbers. In this case, you will get ALL continents and the country names that appear first per continent.*

```sql
SELECT SUM(population)
FROM world
```
You can use **SUM** to **SUM** the values of a column.

```sql
SELECT COUNT(name)
FROM world
```
You can use **COUNT** to **COUNT** the values of a column.

```sql
SELECT DISTINCT(Country)
FROM world
```
**DISTINCT** will remove the duplicates. *In this case the country name will appear only once, without the distinct, it will retrieve all rows from the column Country.*

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
```
The **GROUP BY** is mandatory when you use an aggregate function such as **SUM** or **COUNT**.
```sql
SELECT title 
FROM movies
ORDER BY year DESC
LIMIT 4
```
**LIMIT** will limit the result from your query. 
*It is usually used to ge top or bottom, for instance the 5 products that sold the most for a given month.*
```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```

Using **CASE WHEN** allow you to categorize the values. 
The format is the following:

**CASE**
  **WHEN** condition1 **THEN** result 1
  **WHEN** condition2 **THEN** result 2
  ...
  **ELSE** result (not covered in the conditions)
**END** (you can use END AS nameofthecolumn)

```sql
SELECT name 
FROM teacher
WHERE dept IS NULL
```
Using **NULL** let you find the missign values, or to exclude them from your query.

  
## SELECT IN SELECT (subquery)

```sql
SELECT name FROM world
WHERE population > (
    SELECT population FROM world
    WHERE name='Russia')
```

This is a **SUBQUERY**. It means you will retrieve the **name** from the table **world** which have a **population** greater than the **population of Russia**.

```sql
SELECT name, continent
FROM world
WHERE continent IN(
      SELECT continent
      FROM world
      WHERE name = 'Argentina'
        OR name = 'Australia')
ORDER BY name
```

This is another example where you will get the **country names** and **continents** of the **countries** that are on the same **continent** than 'Argentina' **OR** 'Australia'.

## JOIN
There are several types of JOINs

| JOIN TYPE       | What does it return                                                      |
| ----------------| -------------------------------------------------------------------------|
| INNER JOIN      | Matching values in **both tables**                                       |
| LEFT JOIN       | **ALL left table** and the **matched records** from the **right** table  |
| RIGHT JOIN      | **ALL right table** and the **matched records** from the **left** table  |
| FULL OUTER JOIN | **ALL records** if there is a match in either left or right table        |

source : [wschools](https://www.w3schools.com/sql/sql_join.asp)

```sql
SELECT goal.player,
  goal.teamid,
  game.stadium,
  game.mdate
FROM goal
JOIN game ON (goal.matchid = game.id)
```

The aim of using **JOIN** is to find values in a table by linking another table on a **common column** (a key).

In your select you need to use **nameofthecolumn.nameofthetable**

In your **JOIN** you need to link the common columns.
JOIN table1 ON (table1.commoncolumn = table2.commoncolumn).

You can also simplify the code and make it shorter that way:

```sql
SELECT go.player,
  go.teamid,
  ga.stadium,
  ga.mdate
FROM goal go
JOIN game ga ON (goal.matchid = game.id)
```

After the name of the table you can use an **alias** to avoid (no need to use **AS** for this).

```sql
SELECT teacher.name, dept.name
FROM teacher 
INNER JOIN dept ON (teacher.dept = dept.id)
```
```sql
SELECT teacher.name, dept.name
FROM teacher 
LEFT JOIN dept ON (teacher.dept = dept.id)
```
```sql
SELECT teacher.name, dept.name
FROM teacher 
RIGHT JOIN dept ON (teacher.dept = dept.id)
```
As seen above, the type of **JOIN** used, will lead to **different results**. *(see the output from SQLZOO website).*



The expression "common columns" is not correct. We need to use **primary keys** and **foreign keys**.

| KEY              | Definition                                                                     |
| -----------------|--------------------------------------------------------------------------------|
| PRIMARY KEY (PK) | Unique identifier for each record in a table                                   |
| FOREIGN KEY (FK) | Establish a relationship between tables by referencing the PK of another table |

In our example the primary key for the table game is the game.id and for goal is the goal.id *(details of the table in the SQLZOO exercises).*

```sql
SELECT actor.name 
FROM actor 
JOIN casting ON (actor.id = casting.actorid)
JOIN movie ON (movie.id = casting.movieid)
WHERE movie.title = 'Alien'
```

You can use multiple **JOINs** in the same query. Not every tables are linked together by a foreign key. 

*Let's take an example: You have for instance a **table1** that is **linked** to a **table 2** and a **table 3**. But **table2** and **table3** are **not linked** to each other. By **connecting** in the same query the **3 tables** you can have the information needed (e.g.: you don't need any value from the table1, but you still need to include it in the join if you want to connect values from table2 and table 3).*

### That's it for the SQL basics.
