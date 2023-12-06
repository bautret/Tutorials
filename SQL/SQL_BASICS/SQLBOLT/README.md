# SQLBOLT ANSWERS

Answers to [SQLBolt](https://sqlbolt.com/). Similar to SQLZOO with additional topics.

[SELECT](#SELECT) <br />
[CONSTRAINTS](#CONSTRAINTS) <br />
[FILTERING AND SORTING](#FILTERING_AND_SORTING) <br />
[JOINS](#JOINS) <br />
[OUTER JOINS](#OUTER_JOINS) <br />
[NULLS](#NULLS)<br />
[EXPRESSIONS](#EXPRESSIONS)  <br />
[AGGEGATES](#AGGEGATES) <br />
[ORDER OF EXECUTION](#ORDER_OF_EXECUTION) <br />
[INSERT ROWS](#INSERT_ROWS) <br />
[UPDATE ROWS](#UPDATE_ROWS) <br />
[DELETE ROWS](#DELETE_ROWS) <br />
[CREATING TABLES](#CREATING_TABLES) <br />
[ALTERING TABLES](#ALTERING_TABLES) <br />
[DROPPING TABLES](#DROPPING_TABLES) <br />

## SELECT
```sql
SELECT title
FROM movies
```
```sql
SELECT director 
FROM movies
```
```sql
SELECT title, 
    director 
FROM movies
```
```sql
SELECT title, 
    year 
FROM movies
```
```sql
SELECT * 
FROM movies
```
```sql
SELECT * 
FROM north_american_cities
WHERE country = 'Canada'
```
```sql
SELECT city
FROM north_american_cities
WHERE country = 'United States'
ORDER BY latitude DESC
```
```sql
SELECT city, 
    longitude 
FROM north_american_cities
WHERE longitude <(
    SELECT city
    FROM north_american_cities
    WHERE city = 'Chicago')
ORDER BY longitude ASC
```
```sql
SELECT city 
FROM north_american_cities
WHERE country = 'Mexico'
ORDER BY population DESC
LIMIT 2
```
```sql
SELECT city,
    population
FROM north_american_cities
WHERE country = 'United States'
ORDER BY population DESC
LIMIT 2
OFFSET 2
```
## CONSTRAINTS
```sql
SELECT * 
FROM movies
WHERE id = 6
```
```sql
SELECT * 
FROM movies
WHERE year BETWEEN 2000 AND 2010
```
```sql
SELECT * 
FROM movies
WHERE year NOT BETWEEN 2000 AND 2010
```
```sql
SELECT * 
FROM movies
WHERE title LIKE '%Toy%'
```
```sql
SELECT * 
FROM movies
WHERE director = 'John Lasseter'
```
```sql
SELECT * 
FROM movies
WHERE director IS NOT 'John Lasseter'
```
```sql
SELECT * 
FROM movies
WHERE title LIKE '%WALL%'
```
## FILTERING AND SORTING
```sql
SELECT DISTINCT(director) 
FROM movies
ORDER BY director
```
```sql
SELECT title 
FROM movies
ORDER BY year DESC
LIMIT 4
```
```sql
SELECT title 
FROM movies
ORDER BY title
LIMIT 5
```
```sql
SELECT title
FROM movies
ORDER BY title ASC
LIMIT 5
OFFSET 5
```
## JOINS
```sql
SELECT m.title, 
    bo.domestic_sales,
    bo.international_sales
FROM movies m
JOIN boxoffice bo ON (m.id = bo.movie_id)
```
```sql
SELECT m.title,
    bo.international_sales,
    bo.domestic_sales
FROM movies m
JOIN boxoffice bo ON (m.id = bo.movie_id)
WHERE bo.international_sales > bo.domestic_sales
```
```sql
SELECT m.title
FROM movies m
JOIN boxoffice bo ON (m.id = bo.movie_id)
ORDER BY bo.rating DESC
```
## OUTER JOINS
```sql
SELECT DISTINCT building 
FROM employees
```
```sql
SELECT * 
FROM buildings
```
```sql
SELECT DISTINCT(building_name), 
    role 
FROM buildings 
LEFT JOIN employees ON (building_name = building)
```
## NULLS
```sql
SELECT name,
    role
FROM employees
WHERE building IS NULL
```
```sql
SELECT DISTINCT b.building_name
FROM buildings b
LEFT JOIN employees e ON (b.building_name = e.building)
WHERE e.role IS NULL
```
## EXPRESSIONS
```sql
SELECT m.title,
    ROUND((bo.domestic_sales + bo.international_sales) / 1000000,0) AS total_Sales_Millions
FROM movies m
JOIN boxoffice bo ON (m.id = bo.movie_id)
```
```sql
SELECT m.title,
    ((bo.rating) * 10) AS Rating_Percent
FROM movies m
JOIN boxoffice bo ON (m.id = bo.movie_id)
```
```sql
SELECT title,
    year
FROM movies
WHERE year % 2 == 0
```
## AGGEGATES

```sql
SELECT name,
    MAX(Years_employed)
FROM employees
```
```sql
SELECT role, 
    AVG(years_employed) AS Average_Years_Employed
FROM employees
GROUP BY role
```
```sql
SELECT building, 
    SUM(years_employed) 
FROM employees
GROUP BY building
```
```sql
SELECT role,
    COUNT(*) AS Number_Of_Artists
FROM employees
WHERE role = "Artist"
```
```sql
SELECT role,
    COUNT(name) AS Number_Of_Employees 
FROM employees
GROUP BY role
```
```sql
SELECT role,
	SUM(Years_employed) AS Total_Years_Accumulated
FROM employees
WHERE role = 'Engineer'
```
## ORDER OF EXECUTION
```sql
SELECT m.director,
count(m.title)
FROM movies m
GROUP BY director
```
```sql
SELECT m.director,
    SUM(bo.domestic_sales + bo.international_sales) AS total_Sales
FROM movies m
JOIN boxoffice bo ON (m.id = bo.movie_id)
GROUP BY director
```
## INSERT ROWS
```sql
INSERT INTO movies 
VALUES (4, 
    "Toy Story 4", 
    "El Directore", 
    2015, 
    90)
```
```sql
INSERT INTO boxoffice 
VALUES (4, 
    8.7, 
    340000, 
    270000)
```
## UPDATE ROWS
```sql
UPDATE movies
SET director = "John Lasseter"
WHERE id = 2
```
```sql
UPDATE movies
SET year = 1999
WHERE id = 3
```
```sql
UPDATE movies
SET director = "Lee Unkrich",
    title = "Toy Story 3"
WHERE id = 11
```
## DELETE ROWS
```sql
DELETE FROM Movies
WHERE year < 2005
```
```sql
DELETE FROM Movies
WHERE director = "Andrew Stanton"
```
## CREATING TABLES
```sql
CREATE TABLE Database (
    Name TEXT,
    Version FLOAT,
    Download_count INTEGER)
```
## ALTERING TABLES
```sql
ALTER TABLE Movies
ADD Aspect_ratio FLOAT
```
```sql
ALTER TABLE Movies
ADD Language TEXT
    DEFAULT English
```
## DROPPING TABLES
```sql
DROP TABLE movies
```
```sql
DROP TABLE boxoffice
```
