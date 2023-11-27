# SQLZOO ANSWERS

Answers to [SQLZOO challenges](https://sqlzoo.net/wiki/SQL_Tutorial). A practical and fun way to learn SQL.

*answer to very last question missing (Self JOIN : 10)*

Structure inspired by [codyloyd](https://github.com/codyloyd/sqlzoo-solutions/blob/master/SQLZOO_solutions.md).

[SELECT basics](#SELECT-basics)  <br />
[SELECT from world](#SELECT-from-world)  <br />
[SELECT from nobel](#SELECT-from-nobel)  <br />
[SELECT in SELECT](#SELECT-in-SELECT)  <br />
[SUM and COUNT](#SUM-and-COUNT)  <br />
[JOIN](#JOIN)  <br />
[MORE JOIN](#MORE-JOIN)  <br />
[Using NULL](#Using-NULL)  <br />
[Self JOIN](#Self-JOIN)

## SELECT basics
1.
```sql
SELECT population
FROM world
WHERE name = 'Germany'
```
2.
```sql
SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark')
```
3.
```sql
SELECT name,
  area
FROM world
WHERE area BETWEEN 200000 AND 250000
```

## SELECT from world
1.
```sql
SELECT name,
  continent,
  population 
FROM world
```SELECT s.id,
s.name
FROM stops s
JOIN route r ON (s.id = r.stop)
WHERE r.num = '4'
AND r.company = 'LRT'
2.
```sql
SELECT name
FROM world
WHERE population >= 200000000
```
3.
```sql
SELECT name,
  gdp/population 
FROM world
WHERE population >= 200000000
```
4.
```sql
SELECT name,
  population/1000000
FROM world
WHERE continent = 'South America'
```
5.
```sql
SELECT name,
  population
FROM world
WHERE name IN ('France', 'Germany', 'Italy')
```
6.
```sql
SELECT name
FROM world
WHERE name LIKE '%United%'
```
7.
```sql
SELECT name,
  population,
  area
FROM world
WHERE area > 3000000 OR population > 250000000
```
8.
```sql
SELECT name,
  population,
  area
FROM world
WHERE population > 250000000 XOR area > 3000000
```
9.
```sql
SELECT name,
  round(population/1000000,2) AS population,
  round(GDP/1000000000,2) AS GDP
FROM world
WHERE continent = 'South America'
```
10.
```sql
SELECT name,
  round(GDP/population, -3)
FROM world
WHERE GDP >= 1000000000000
```
11.
```sql
SELECT name,
  capital
FROM world
WHERE LENGTH(name) = LENGTH(capital)
```
12.
```sql
SELECT name,
  capital
FROM world
WHERE LEFT(capital, 1) = LEFT(name, 1)
  AND name <> capital
```
13.
```sql
SELECT name
FROM world
WHERE name LIKE '%a%'
  AND name LIKE '%e%'
  AND name LIKE '%i%'
  AND name LIKE '%o%'
  AND name LIKE '%u%'
  AND name NOT LIKE '% %';
```
## SELECT from nobel
1.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950
```
2.
```sql
SELECT winner
FROM nobel
WHERE yr = 1962
  AND subject = 'literature'
```
3.
```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```
4.
```sql
SELECT winner
FROM nobel
WHERE subject = 'peace'
  AND yr >= 2000
```
5.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'literature'
  AND yr BETWEEN 1980 AND 1989
```
6.
```sql
SELECT * FROM nobel
WHERE winner IN ('Theodore Roosevelt',
                  'Thomas Woodrow Wilson',
                  'Jimmy Carter', 
                  'Barack Obama')
```
7.
```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%'
```
8.
```sql
SELECT *
FROM nobel
WHERE yr = 1980 AND subject = 'physics'
  OR yr = 1984 AND subject = 'chemistry'
```
9.
```sql
SELECT *
FROM nobel
WHERE yr = 1980
  AND subject NOT IN ('chemistry', 'medicine')
```
10.
```sql
SELECT *
FROM nobel
WHERE yr < 1910 AND subject = 'Medicine'
  OR yr >= 2004 AND subject = 'Literature'
```
11.
```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG'
```
12.
```sql
SELECT *
FROM nobel
WHERE winner = '%EUGENE O%'
```
13.
```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner
```
14.
```sql
SELECT winner, subject 
FROM nobel
WHERE yr = 1984
ORDER BY subject IN('physics','chemistry'),
                      subject,
                      winner 
```
## SELECT in SELECT
1.
```sql
SELECT name FROM world
WHERE population >(
        SELECT population FROM world
        WHERE name='Russia')
```
2.
```sql
SELECT name FROM world
WHERE continent = 'Europe'
AND GDP/population >(
        SELECT GDP/population FROM world
        WHERE name='United Kingdom')
```
3.
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
4.
```sql
SELECT name, population
FROM world
WHERE population >(
        SELECT population
        FROM world
        WHERE name = 'United Kingdom')
  AND population <(
        SELECT population
        FROM world
        WHERE name = 'Germany')
```
5.
```sql
SELECT name,
CONCAT(CAST(round(population/(SELECT population FROM world WHERE name = 'Germany'),2)*100 AS INT), '%') AS percentage
FROM world
WHERE continent = 'Europe'
```
6.
```sql
SELECT name
FROM world 
WHERE gdp > ALL
      (SELECT gdp FROM world WHERE continent = 'Europe')
```
7.
```sql
SELECT continent, name, area 
FROM world x
WHERE area >= ALL(
        SELECT area FROM world y
        WHERE y.continent = x.continent
        AND area > 0)
```
8.
```sql
SELECT continent, MIN(name) AS name
FROM world
GROUP BY continent
ORDER BY name
```
9.
```sql
SELECT w.name, w.continent, w.population
FROM world w
WHERE population <= 25000000
AND w.continent NOT IN(
        SELECT DISTINCT w2.continent
        FROM world w2
        WHERE w2.population > 25000000)
```
10.
```sql
SELECT name, continent
FROM world x
WHERE population >= ALL (
        SELECT population*3
        FROM world y
        WHERE x.continent = y.continent
        AND y.name != x.name)
```

## SUM and COUNT
1.
```sql
SELECT SUM(population) AS total_population
FROM world
```
2.
```sql
SELECT DISTINCT continent
FROM world
```
3.
```sql
SELECT SUM(GDP)
FROM world
WHERE continent = 'Africa'
```
4.
```sql
SELECT COUNT(name)
FROM world
WHERE area >= 1000000
```
5.
```sql
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```
6.
```sql
SELECT DISTINCT continent, COUNT(name)
FROM world
GROUP BY continent
```
7.
```sql
SELECT DISTINCT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent
```
8.
```sql
SELECT DISTINCT(continent)
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000
```
## JOIN
1.
```sql
SELECT matchid,
  player
FROM goal 
WHERE teamid = 'GER'
```
2.
```sql
SELECT id,
  stadium,
  team1,
  team2
FROM game
WHERE id = 1012
```
3.
```sql
SELECT goal.player,
  goal.teamid,
  game.stadium,
  game.mdate
FROM goal
JOIN game ON (goal.matchid = game.id)
WHERE goal.teamid = 'GER'
```
4.
```sql
SELECT game.team1,
  game.team2,
  goal.player
FROM game
JOIN goal ON (game.id = goal.matchid)
WHERE goal.player LIKE 'Mario%'
```
5.
```sql
SELECT goal.player,
  goal.teamid,
  eteam.coach,
  goal.gtime
FROM goal
JOIN eteam ON (goal.teamid = eteam.id)
WHERE goal.gtime <= 10
```
6.
```sql
SELECT game.mdate,
  eteam.teamname
FROM game
JOIN eteam ON (game.team1 = eteam.id)
WHERE eteam.coach = 'Fernando Santos
```
7.
```sql
SELECT goal.player
FROM goal
JOIN game ON (game.id = goal.matchid)
WHERE game.stadium = 'National Stadium, Warsaw'
```
8.
```sql
SELECT DISTINCT(goal.player)
FROM goal
JOIN game ON (game.id = goal.matchid)
WHERE (game.team2 = 'GER' OR game.team1 = 'GER')
AND goal.teamid != 'GER'
```
9.
```sql
SELECT DISTINCT(eteam.teamname),
  COUNT(goal.gtime)
FROM eteam
JOIN goal ON (eteam.id = goal.teamid)
GROUP BY eteam.teamname
```
10.
```sql
SELECT DISTINCT(game.stadium),
  COUNT(goal.gtime)
FROM game
JOIN goal ON (game.id = goal.matchid) 
GROUP BY game.stadium
```
11.
```sql
SELECT goal.matchid,
  game.mdate,
  COUNT(goal.teamid)
FROM goal
JOIN game ON (game.id = goal.matchid)
WHERE game.team1 = 'POL' OR game.team2 = 'POL'
GROUP BY goal.matchid
```
12.
```sql
SELECT goal.matchid,
  game.mdate,
  COUNT(goal.gtime)
FROM goal
JOIN game ON (game.id = goal.matchid)
WHERE goal.teamid = 'GER'
GROUP BY goal.matchid
```
13.
```sql
SELECT DISTINCT(game.mdate), 
  game.team1, 
  SUM(CASE WHEN game.team1 = goal.teamid THEN 1 ELSE 0 END) score1,
  game.team2,
  SUM(CASE WHEN game.team2 = goal.teamid THEN 1 ELSE 0 END) score2
FROM game
JOIN goal ON (game.id = goal.matchid)
GROUP BY game.mdate,
  goal.matchid,
  game.team1,
  game.team2
ORDER BY game.mdate,
  goal.matchid,
  game.team1,
  game.team2
```
## More JOIN
1.
```sql
SELECT id, title
FROM movie
WHERE yr = 1962
```
2.
```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane'
```
3.
```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr
```
4.
```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```
5.
```sql
SELECT id
FROM movie
WHERE title = 'Casablanca'
```
6.
```sql
SELECT actor.name 
FROM actor 
JOIN casting ON (actor.id = casting.actorid)
WHERE casting.movieid = 11768
```
7.
```sql
SELECT actor.name 
FROM actor 
JOIN casting ON (actor.id = casting.actorid)
JOIN movie ON (movie.id = casting.movieid)
WHERE movie.title = 'Alien'
```
8.
```sql
SELECT movie.title
FROM movie
JOIN casting ON (casting.movieid = movie.id)
JOIN actor ON (casting.actorid = actor.id)
WHERE actor.name = 'Harrison Ford'
```
9.
```sql
SELECT movie.title
FROM movie
JOIN casting ON (casting.movieid = movie.id)
JOIN actor ON (casting.actorid = actor.id)
WHERE actor.name = 'Harrison Ford' 
  AND casting.ord != '1'
```
10.
```sql
SELECT movie.title,
  actor.name
FROM movie
JOIN casting ON (movie.id = casting.movieid)
JOIN actor ON (actor.id = casting.actorid)
WHERE movie.yr = '1962'
  AND casting.ord = '1'
```
11.
```sql
SELECT yr,
  COUNT(title) 
FROM movie 
JOIN casting ON (movie.id = movieid)
JOIN actor ON (actorid = actor.id)
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```
12.
```sql
SELECT title,
  name
FROM movie
  JOIN casting ON (movieid = movie.id AND ord = 1)
  JOIN actor ON (actorid = actor.id)
WHERE movie.id IN(
        SELECT movieid 
        FROM casting
        WHERE actorid IN(
            SELECT id
            FROM actor
            WHERE name = 'Julie Andrews'))
```
13.
```sql
SELECT name
FROM actor
JOIN casting ON actor.id = casting.actorid
WHERE ord = 1
GROUP BY name
HAVING COUNT(name) >= 15;
```
14.
```sql
SELECT title,
  COUNT(name) AS nbr_actors
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE yr = 1978
GROUP BY title
ORDER BY COUNT(name) DESC,
  title
```
15.
```sql
SELECT DISTINCT name
FROM actor
JOIN casting ON actor.id = casting.actorid
WHERE name <> 'Art Garfunkel'
AND movieid IN (
                SELECT movieid
                FROM actor
                JOIN casting ON actor.id = casting.actorid
                WHERE name = 'Art Garfunkel')
```
## Using NULL
1.
```sql
SELECT name 
FROM teacher
WHERE dept IS NULL
```
2.
```sql
SELECT teacher.name, dept.name
FROM teacher 
INNER JOIN dept ON (teacher.dept = dept.id)
```
3.
```sql
SELECT teacher.name, dept.name
FROM teacher 
LEFT JOIN dept ON (teacher.dept = dept.id)
```
4.
```sql
SELECT teacher.name, dept.name
FROM teacher 
RIGHT JOIN dept ON (teacher.dept = dept.id)
```
5.
```sql
SELECT name, 
  COALESCE(mobile, '07986 444 2266')
FROM teacher
```
6.
```sql
SELECT t.name, 
COALESCE(d.name, 'None')
FROM teacher t
LEFT JOIN dept d ON t.dept = d.id;
```
7.
```sql
SELECT COUNT(name) AS number_of_teachers,
COUNT(mobile) AS number_of_mobile_phones
FROM teacher
```
8.
```sql
SELECT d.name,
COUNT(t.dept)
FROM teacher t
RIGHT JOIN dept d ON (d.id = t.dept)
GROUP BY d.name
```
9.
```sql
SELECT name, 
  CASE WHEN dept IN ('1', '2') THEN 'Sci' ELSE 'Art' END
FROM teacher
```
10.
```sql
SELECT name, 
  CASE WHEN dept IN ('1', '2') THEN 'Sci'
  WHEN dept IN ('#') THEN 'Art' 
  ELSE 'None' END
FROM teacher
```
## Self JOIN
1.
```sql
SELECT COUNT(DISTINCT(stop))
FROM route
```
2.
```sql
SELECT id
FROM stops
WHERE name = 'Craiglockhart'
```
3.
```sql
SELECT s.id,
  s.name
FROM stops s
JOIN route r ON (s.id = r.stop)
WHERE r.num = '4'
  AND r.company = 'LRT'
```
4.
```sql
SELECT company, 
  num, 
COUNT(*)
FROM route 
WHERE stop=149 
  OR stop=53
GROUP BY company, 
  num
HAVING COUNT(*) = 2
```
5.
```sql
SELECT a.company,
  a.num,
  a.stop,
  b.stop
FROM route a 
JOIN route b ON (a.company = b.company
  AND a.num = b.num)
WHERE a.stop=53
  AND b.stop = '149'
```
6.
```sql
SELECT a.company,
  a.num,
  stopa.name,
  stopb.name
FROM route a
JOIN route b ON (a.company=b.company
  AND a.num=b.num)
JOIN stops stopa ON (a.stop=stopa.id)
JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart'
  AND stopb.name='London Road'
```
7.
```sql
SELECT DISTINCT R1.company, R1.num
FROM route R1, 
  route R2
WHERE R1.num = R2.num 
  AND R1.company = R2.company
  AND R1.stop = '115' 
  AND R2.stop = '137'
```
8.
```sql
SELECT a.company,
  a.num
FROM route a 
  JOIN route b ON (a.company = b.company AND a.num = b.num)
  JOIN stops stopa ON (a.stop = stopa.id)
  JOIN stops stopb ON (b.stop = stopb.id)
WHERE stopa.name = 'Craiglockhart'
  AND stopb.name = 'Tollcross'
```
9.
```sql
SELECT DISTINCT S2.name,
  R2.company,
  R2.num
FROM stops S1,
  stops S2,
  route R1,
  route R2
WHERE S1.name = 'Craiglockhart'
  AND S1.id = R1.stop
  AND R1.company = R2.company 
  AND R1.num = R2.num
  AND R2.stop = S2.id;
```
10.
```sql

```
