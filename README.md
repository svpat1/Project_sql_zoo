# Project_sql_zoo

https://sqlzoo.net/wiki/SQL_Tutorial


SELECT basics
#1 SELECT population 
    FROM world
     WHERE name = 'Germany'
   
#2 SELECT name, population
    FROM world
     WHERE name IN ('Sweden', 'Norway', 'Denmark');   
   
#3 SELECT name, area
    FROM world
     WHERE area BETWEEN 200000 AND 250000
  
SELECT names
#1 SELECT population 
    FROM world
     WHERE name = 'Germany'

#2 SELECT name, population 
    FROM world
     WHERE name IN ('Sweden', 'Norway', 'Denmark');
  
#3 SELECT name, area 
    FROM world
     WHERE area BETWEEN 200000 AND 250000
  
SELECT from WORLD Tutorial
#1 SELECT name, continent, population 
    FROM world

#2 SELECT name 
    FROM world
     WHERE population >= 200000000

#3 SELECT name, GDP/population AS 'per capita GDP'
    FROM world
     WHERE population >= 200000000

#4 SELECT name, population/1000000 AS 'population in milions'
    FROM world
     WHERE continent = 'South America'

#5 SELECT name, population
    FROM world
     WHERE name IN ('France','Germany','Italy')

#6 SELECT name
    FROM world
     WHERE name LIKE 'United%'

#7 SELECT name, population, area
    FROM world
     WHERE area >= 3000000 
      OR population >= 250000000

#8 SELECT name, population, area
    FROM world
     WHERE area >= 3000000 xor population >= 250000000 

#9 SELECT name, ROUND(population/1000000,2) AS 'population in millions', ROUND(GDP/1000000000,2) AS 'GDP in billions'
    FROM world
     WHERE continent = 'South America'

#10 SELECT name, ROUND(GDP/population,-3) AS 'per capita GDP'
     FROM world
      WHERE GDP >= 1000000000000

#11 SELECT name, capital
     FROM world
      WHERE LENGTH(name) = LENGTH(capital)

#12 SELECT name, capital
     FROM world
      WHERE LEFT(name,1) = LEFT(capital,1)
       AND name <> capital

#13 SELECT name
     FROM world
      WHERE name LIKE '%a%' 
       AND name LIKE '%e%' 
        AND name LIKE '%i%' 
         AND name LIKE '%o%' 
          AND name LIKE '%u%'
           AND name NOT LIKE '% %'
 
SELECT from Nobel Tutorial
#1 SELECT yr, subject, winner
    FROM nobel
     WHERE yr = 1950

#2 SELECT winner
    FROM nobel
     WHERE yr = 1962
      AND subject = 'Literature'
   
#3 SELECT yr, subject
    FROM nobel
     WHERE winner = 'Albert Einstein'

#4 SELECT winner
    FROM nobel
     WHERE subject = 'Peace'
      AND yr >= 2000
 
#5 SELECT *
    FROM nobel
     WHERE (subject = 'Literature') 
      AND (yr BETWEEN 1980 AND 1989)

#6 SELECT * FROM nobel
    WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter', 
                  'Barack Obama')

#7 SELECT winner
    FROM nobel
     WHERE winner LIKE 'John%'

#8 SELECT yr, subject, winner
    FROM nobel
     WHERE subject = 'Physics' AND yr = 1980
      OR subject = 'Chemistry' AND yr = 1984

#9 SELECT yr, subject, winner
    FROM nobel
     WHERE yr = 1980 AND subject NOT IN ('Chemistry', 'Medicine')

#10 SELECT yr, subject, winner
     FROM nobel
      WHERE subject = 'Medicine' AND yr < 1910
       OR subject = 'Literature' AND yr >= 2004

#11 SELECT * 
     FROM nobel
      WHERE winner LIKE 'Peter Gr_nberg'

#12 SELECT *
     FROM nobel
      WHERE winner = 'Eugene O''neill'

#13 SELECT winner, yr, subject
     FROM nobel
      WHERE winner LIKE 'Sir%'
       ORDER BY yr desc, winner 

#14 SELECT winner, subject 
     FROM nobel
      WHERE yr=1984
       ORDER BY subject IN ('Physics','Chemistry'),subject,winner
 
 SELECT within SELECT Tutorial
 #1 SELECT name FROM world
     WHERE population >
      (SELECT population FROM world
        WHERE name='Russia')
      
 #2 SELECT name
     FROM world
      WHERE continent = 'Europe' 
       AND GDP/population > (SELECT GDP/population
                              FROM world 
                               WHERE name = 'United Kingdom') 
    
 #3 SELECT name, continent
     FROM world
      WHERE continent IN (select continent from world where name in ('Argentina', 'Australia'))
       ORDER BY name

#4 SELECT name, population
    FROM world
     WHERE population > (SELECT population
                          FROM world 
                           WHERE name = 'Canada') 
      AND population < (SELECT population
                         FROM world 
                          WHERE name = 'Poland')

#5 SELECT name, CONCAT(ROUND(100*population/(SELECT population
                                              FROM world
                                               WHERE name = 'Germany')
                      ), '%')
    FROM world
     WHERE continent = 'Europe'

#6 SELECT name
    FROM world
     WHERE GDP > ALL(SELECT GDP 
                      FROM world 
                       WHERE GDP>0 
                        AND continent = 'Europe')

#7 SELECT continent, name, area 
    FROM world x
     WHERE area >= ALL
      (SELECT area 
        FROM world y
         WHERE y.continent=x.continent
          AND area>0)

#8 SELECT continent, name 
    FROM world x
     WHERE name <= ALL (SELECT name   
                         FROM world y 
                          WHERE x.continent = y.continent) 

#9 SELECT name, continent, population
    FROM world x
     WHERE 25000000 > ALL(SELECT population 
                           FROM world y 
                            WHERE x.continent=y.continent 
                             AND population > 0
                         )

#10 SELECT name, continent
     FROM world x
      WHERE population/3 >= ALL (SELECT population 
                                  FROM world y 
                                   WHERE x.continent=y.continent 
                                    AND population > 0
                                     AND name NOT IN (SELECT name 
                                                       FROM world x
                                                        WHERE population >= ALL(SELECT population 
                                                                                 FROM world y
                                                                                  WHERE y.continent=x.continent
                                                                                   AND  population > 0)))

SUM and COUNT
#1 SELECT SUM(population)
    FROM world

#2 SELECT DISTINCT continent
    FROM world

#3 SELECT SUM(GDP)
    FROM world
     WHERE continent = 'Africa'

#4 SELECT COUNT(name)
    FROM world
     WHERE area > 1000000

#5 SELECT SUM(population)
    FROM world
     WHERE name IN ('Estonia', 'Latvia', 'Lithuania')

#6 SELECT continent, COUNT(name) 
    FROM world
     GROUP BY continent

#7 SELECT continent, COUNT(name)
    FROM world
     WHERE population > 10000000
      GROUP BY continent

#8 SELECT continent
    FROM world
     GROUP BY continent
      HAVING SUM(population) > 100000000

The JOIN operation
#1 SELECT matchid, player 
    FROM goal 
     WHERE teamid = 'GER'
  
#2 SELECT id,stadium,team1,team2
    FROM game
     WHERE id = 1012

#3 SELECT player, teamid, stadium, mdate 
    FROM game 
     JOIN goal ON (game.id=goal.matchid)
      WHERE teamid = 'GER'

#4 SELECT team1, team2, player
    FROM game 
     JOIN goal ON (game.id=goal.matchid)
      WHERE player LIKE 'Mario%'

#5 SELECT player, teamid, coach, gtime
    FROM goal 
     JOIN eteam ON goal.teamid = eteam.id 
      WHERE gtime<=10
 
#6 SELECT mdate, teamname 
    FROM game 
     JOIN eteam ON team1 = eteam.id
      WHERE coach = 'Fernando Santos' 

#7 SELECT player
    FROM goal 
     JOIN game ON goal.matchid = game.id
      WHERE stadium = 'National Stadium, Warsaw'

#8 SELECT DISTINCT player
    FROM goal 
     JOIN game ON goal.matchid = game.id
      WHERE teamid != 'GER'
       AND (game.team1 = 'Ger' OR game.team2 = 'Ger')

#9 SELECT teamname, COUNT(gtime)
    FROM eteam 
     JOIN goal ON id=teamid
      GROUP BY teamname

#10 SELECT stadium, COUNT(gtime)
     FROM game 
      JOIN goal ON id = matchid
       GROUP BY stadium

#11 SELECT matchid, mdate, COUNT(teamid)
     FROM game 
      JOIN goal ON goal.matchid = game.id 
       WHERE (team1 = 'Pol' OR team2 = 'Pol')
        GROUP BY matchid, mdate

#12 SELECT matchid, mdate, COUNT(teamid)
     FROM goal JOIN game ON matchid = id 
      WHERE teamid = 'GER'
       GROUP BY matchid, mdate

#13 SELECT mdate, team1, SUM(CASE WHEN teamid=team1 THEN 1 
                                  ELSE 0 
                             END) score1, team2, SUM(CASE WHEN teamid = team2 THEN 1 
                                                          ELSE 0 END) score2
     FROM game 
      LEFT JOIN goal ON matchid = id
       GROUP BY mdate, team1, team2
        ORDER BY mdate, matchid

More JOIN operations
#1 SELECT id, title
    FROM movie
     WHERE yr=1962
 
#2 SELECT yr
    FROM movie
     WHERE title = 'Citizen Kane'

#3 SELECT id, title, yr
    FROM movie
     WHERE title LIKE 'Star Trek%'
      ORDER BY yr

#4 SELECT id
    FROM actor
     WHERE name = 'Glenn Close'

#5 SELECT id
    FROM movie
     WHERE title = 'Casablanca'

#6 SELECT name
    FROM actor 
     JOIN casting ON actor.id = casting.actorid
      WHERE movieid = 11768

#7 SELECT name
    FROM actor 
     JOIN casting ON actor.id = casting.actorid
      WHERE movieid = (SELECT id FROM movie WHERE title = 'Alien')

#8 SELECT title
    FROM movie 
     JOIN casting ON movie.id = casting.movieid
      WHERE actorid = (SELECT id FROM actor WHERE name = 'Harrison Ford')

#9 SELECT title
    FROM movie 
     JOIN casting ON movie.id = casting.movieid
      WHERE actorid = (SELECT id FROM actor WHERE name = 'Harrison Ford')
       AND ord != 1

#10 SELECT title, name
     FROM movie 
      JOIN casting ON movie.id = casting.movieid
       JOIN actor ON actor.id = casting.actorid
        WHERE yr = 1962
         AND ord = 1 

#11 SELECT yr,COUNT(title)
     FROM movie 
      JOIN casting ON movie.id=movieid
       JOIN actor ON actorid=actor.id
        WHERE name='John Travolta'
         GROUP BY yr
          HAVING COUNT(title)=(SELECT MAX(c) 
                                FROM (SELECT yr,COUNT(title) AS c 
                                       FROM movie 
                                        JOIN casting ON movie.id=movieid
                                         JOIN actor ON actorid=actor.id
                                          WHERE name='John Travolta'
                                           GROUP BY yr) AS t)

#12 SELECT title, name
     FROM movie 
      JOIN casting ON movie.id = casting.movieid
       JOIN actor ON actor.id = casting.actorid
        WHERE movie.id IN (SELECT movieid 
                            FROM casting 
                             WHERE actorid IN (SELECT id 
                                                FROM actor 
                                                 WHERE name='Julie Andrews'))
         AND ord = 1

#13 SELECT name 
     FROM actor 
      WHERE id IN (SELECT actorid 
                    FROM casting 
                     WHERE ord = 1 
                      GROUP BY actorid 
                       HAVING COUNT(actorid)>=30)

#14 SELECT title,COUNT(actorid)
     FROM casting JOIN movie ON movie.id = casting.movieid
      WHERE yr = 1978
       GROUP BY title
        ORDER BY COUNT(actorid) DESC, title

#15 SELECT DISTINCT name
     FROM casting 
      JOIN actor ON actor.id = casting.actorid
       WHERE movieid IN (SELECT movieid 
                          FROM casting 
                           WHERE actorid = (SELECT id 
                                             FROM actor 
                                              WHERE name = 'Art Garfunkel'))
        AND name != 'Art Garfunkel'

Using Null
#1 SELECT name
    FROM teacher
     WHERE dept IS NULL

#2 SELECT teacher.name, dept.name
    FROM teacher 
     INNER JOIN dept ON (teacher.dept=dept.id)

#3 SELECT teacher.name, dept.name
    FROM teacher 
     LEFT JOIN dept ON (teacher.dept=dept.id)
        
#4 SELECT teacher.name, dept.name
    FROM teacher 
     RIGHT JOIN dept ON (teacher.dept=dept.id)
           
#5 SELECT name, COALESCE(mobile,'07986 444 2266') AS mobile
    FROM teacher 

#6 SELECT teacher.name, COALESCE(dept.name, 'None')
    FROM teacher 
     LEFT OUTER JOIN dept ON (teacher.dept=dept.id)

#7 SELECT COUNT(name), COUNT(mobile)
    FROM teacher

#8 SELECT dept.name, COUNT(teacher.id)
    FROM teacher 
     RIGHT JOIN dept ON (teacher.dept = dept.id)
      GROUP BY dept.name

#9 SELECT teacher.name, CASE WHEN dept = 1 or dept = 2 THEN 'Sci'
                             ELSE 'Art'
                        END 
    FROM teacher 
     LEFT JOIN dept ON (teacher.dept = dept.id)

#10 SELECT teacher.name, CASE WHEN dept = 1 or dept = 2 THEN 'Sci'
                              WHEN dept = 3 THEN 'Art'
                              ELSE 'None'
                         END 
     FROM teacher 
      LEFT JOIN dept ON (teacher.dept = dept.id)

NSS Tutorial
#1 SELECT A_STRONGLY_AGREE
    FROM nss
     WHERE question='Q01'
      AND institution='Edinburgh Napier University'
       AND subject='(8) Computer Science'
   
#2 SELECT institution, subject
    FROM nss
     WHERE question='Q15'
      AND score >=100
   
#3 SELECT institution,score
    FROM nss
     WHERE question='Q15'
      AND subject='(8) Computer Science'
       AND score < 50

#4 SELECT subject, SUM(response)
    FROM nss
     WHERE question='Q22'
      AND (subject='(8) Computer Science'
       OR subject = '(H) Creative Arts and Design')
        GROUP BY subject

#5 SELECT subject, SUM(response*A_STRONGLY_AGREE/100)
    FROM nss
     WHERE question='Q22'
      AND (subject='(8) Computer Science' OR subject = '(H) Creative Arts and Design')
       GROUP BY subject

#6 SELECT subject, ROUND(SUM(response*A_STRONGLY_AGREE)/SUM(response))
    FROM nss
     WHERE question='Q22'
      AND (subject='(8) Computer Science' OR subject = '(H) Creative Arts and Design')
       GROUP BY subject

#7 SELECT institution,ROUND(SUM(response*score)/SUM(response))
    FROM nss
     WHERE question='Q22'
      AND (institution LIKE '%Manchester%')
       GROUP BY institution
        ORDER BY institution

#8 SELECT institution, SUM(sample), SUM(CASE WHEN subject = '(8) Computer Science' THEN sample END) AS 'comp'
    FROM nss
     WHERE question='Q01'
      AND (institution LIKE '%Manchester%')
       GROUP BY institution

Self join
#1 SELECT COUNT(id)
    FROM stops

#2 SELECT id
    FROM stops
     WHERE name = 'Craiglockhart'

#3 SELECT id, name
    FROM stops 
     JOIN route ON stops.id = route.stop
      WHERE num = '4'
       AND company = 'LRT'

#4 SELECT company, num, COUNT(*)
    FROM route 
     WHERE stop=149 OR stop=53
      GROUP BY company, num
       HAVING COUNT(pos) = 2

#5 SELECT a.company, a.num, a.stop, b.stop
    FROM route a 
     JOIN route b ON (a.company=b.company AND a.num=b.num)
      WHERE a.stop=53 
       AND b.stop=149

#6 SELECT a.company, a.num, stopa.name, stopb.name
    FROM route a 
     JOIN route b ON (a.company=b.company AND a.num=b.num)
      JOIN stops stopa ON (a.stop=stopa.id)
       JOIN stops stopb ON (b.stop=stopb.id)
        WHERE stopa.name='Craiglockhart'
         AND stopb.name='London Road'

#7 SELECT a.company,a.num
    FROM route a 
     JOIN route b ON (a.company=b.company AND a.num=b.num)
      WHERE a.stop=115 AND b.stop=137
       GROUP BY a.company, a.num

#8 SELECT a.company, a.num
    FROM route a 
     JOIN route b ON (a.company=b.company AND a.num=b.num)
      JOIN stops stopa ON (a.stop=stopa.id)
       JOIN stops stopb ON (b.stop=stopb.id)
        WHERE stopa.name='Craiglockhart'
         AND stopb.name='Tollcross'

#9 SELECT DISTINCT stopb.name, a.company, a.num
    FROM route a 
     JOIN route b ON (a.company=b.company AND a.num=b.num)
      JOIN stops stopa ON (a.stop=stopa.id)
       JOIN stops stopb ON (b.stop=stopb.id)
        WHERE stopa.name='Craiglockhart'

#10 SELECT start.num, start.company, start.name, end.num, end.company
     FROM (SELECT DISTINCT a.num, a.company,stopb.name 
            FROM route a 
             JOIN route b ON (a.company=b.company AND a.num=b.num)
              JOIN stops stopa ON (a.stop=stopa.id)
               JOIN stops stopb ON (b.stop=stopb.id)
                WHERE stopa.name='Craiglockhart') AS start 
      JOIN (SELECT DISTINCT stopa.name, a.num, a.company 
             FROM route a 
              JOIN route b ON (a.company=b.company AND a.num=b.num)
               JOIN stops stopa ON (a.stop=stopa.id)
                JOIN stops stopb ON (b.stop=stopb.id)
                 WHERE stopb.name='Lochend') AS end
      ON end.name = start.name
       ORDER BY start.num, end.num 

