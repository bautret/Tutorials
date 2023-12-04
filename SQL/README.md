# SQL

From SQLZOO, we can learn the basics of performing SQL queries.

Here is the **[website](https://].net/wiki/SQL_Tutorial)** to review the exercises.
Here are my **[solutions](https://github.com/bautret/Tutorials/tree/main/SQL/SQLZOO)** *(I'd recommend to try by yourself first)*

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

