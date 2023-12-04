# SQL

From SQLZOO, we can learn the basics of performing SQL queries.

Here is the **[website](https://].net/wiki/SQL_Tutorial)** to review the exercises.
Here are my **[solutions](https://github.com/bautret/Tutorials/tree/main/SQL/SQLZOO)** *(I'd recommend to try by yourself first)*

QUICK SUMMARY OF NOTIONS EXPLAINED BELOW

|FUNCTION  |
| ---------|
| SELECT   |

*to update at the very end + add a link to the notion*

## SELECT

```sql
SELECT *
FROM table
```

1. You always want to start a **SQL QUERY** with **SELECT** then the symbol * means **ALL**.
2. You need to get the data from a **TABLE**.

```sql
SELECT column_1,
  column_2
FROM table
```

You don't have to select everything. You can choose the columns that are interesting to you. Each column is separated by a comma, except the last one. You don't have to go to the following line for each new element, but it adds to readability.

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

When you want to filter with several **INPUTS** you use **IN** followed by parentheses and a comma to differentiate each element.

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
You can divide/multiply a column by a number (if the column is containing integers)

```sql
SELECT name,
  GDP/population AS GDP_per_capita
FROM world
```
- You can divide/multiply a column by another column.
- You can rename a column by using **AS** and then the new_name.

```sql
SELECT name,
FROM world
WHERE name LIKE '%United%'
```
If you want to include part of a string in your filter, you can use **%**.

|% position     | What for                                |
| ------------- | --------------------------------------- |
| %text%        | Look if the string contains the text    |
| %text         | Look if the string starts with the text |
| text%         | Look if the string ends with the text   |

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
WHERE (area > 30000000 | population > 25000000) &
      (area < 30000000 & population < 25000000)
```
You can use several operators together.

```sql
WHERE year BETWEEN 2000 AND 2005
```
To specify a range (of dates, quantity etc.) you can use **BETWEEN** number_1 **AND** number_2.

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
You can add several levels of ordering by adding other columns (for name, it will order by ascending alphabetical order).

Important to have in mind the orders of execution.

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
You can decide to set a particular value from a column as **last**. In this case, it will sort results by subject first, then winner **BUT** economics **then** medicine as **last**.

```sql
SELECT continent, MIN(name) AS name
FROM world
```
You can select the **MIN** or **MAX** value. In case of a string it will use alphabetical orders, in case of an integer the minimum/maximum numbers. In this case you will get ALL continents, and the country names that appear first per continent.

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

The expression "common columns" is not correct. We need to use **primary keys** and **foreign keys**.

| KEY              | Definition                                                                     |
| -----------------|--------------------------------------------------------------------------------|
| PRIMARY KEY (PK) | Unique identifier for each record in a table                                   |
| FOREIGN KEY (FK) | Establish a relationship between tables by referencing the PK of another table |

In our example the primary key for the table game is the game.id and for goal is the goal.id (details of the table in the SQLZOO exercises).

ADD SELECT DISTINCT AND GROUP BY (examples in JOIN)
