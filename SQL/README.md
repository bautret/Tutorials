# SQL

From SQLZOO, we can learn the basics of performing SQL queries.

Here is the **[website](https://sqlzoo.net/wiki/SQL_Tutorial)** to review the exercises.
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

You don't have to select everything. You can choose the columns that are interesting to you.

```sql
SELECT column_1, 
  column_2
FROM table
WHERE name = xxx
```

You can filter the data by using **WHERE** and add the sign **=**
- If it is a string, use brackets (e.g.: WHERE country = 'France').
- If it is an integer, you don't need to use brackets (e.g.: WHERE year = 1995).


