# Project_sql_zoo
SELECT basics
#1 SELECT population FROM world
   WHERE name = 'Germany'
   
#2 SELECT name, population FROM world
   WHERE name IN ('Sweden', 'Norway', 'Denmark');   
   
#3 SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
  
SELECT names
#1 SELECT population FROM world
  WHERE name = 'Germany'

#2 SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
  
#3 SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
  
SELECT from WORLD Tutorial
#1 SELECT name, continent, population FROM world

#2 SELECT name FROM world
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
WHERE area >= 3000000 or population >= 250000000

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
WHERE LEFT(name,1) = LEFT(capital,1) AND name <> capital

#13 SELECT name
   FROM world
WHERE name LIKE '%a%' AND name LIKE '%e%' AND name LIKE '%i%' AND name LIKE '%o%' AND name LIKE '%u%'
  AND name NOT LIKE '% %'
