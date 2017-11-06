# Pg Admin 4 query's / Learn Challenge.

### Contributors

  - Morphiee
  - bkiahstroud

# Where Section // WHERE this = this

### What is the population of the US.

  SELECT name, population FROM country WHERE name = 'United States';



### What is the area of the US? (Surface Area)

  SELECT name, surfacearea FROM country WHERE surfacearea > 9000000;



### List countries in Africa that have a population smaller than 30,000,000 and a life expectency of more than 45.

  SELECT name, continent, population, lifeexpectancy FROM country WHERE population < 30000000 and continent = 'Africa' and lifeexpectancy > 45;



### What are countries that are like a republic?

  SELECT name, governmentform FROM country WHERE governmentform like '%Republic%';



### Which countries are some kind of republic and achieved their independence after 1945.

  SELECT name, indepyear, governmentform FROM country WHERE governmentform like '%republic%'' and indepyear > 1945;



### Which countries achieved independence after 1945 that are not some kind of republic?

  SELECT name, indepyear, governmentform FROM country WHERE governmentform not like '%republic%'' and indepyear > 1945;



# Oder by Section // ORDER BY this desc LIMIT #;


### Which fifteen countries have the lowest life expectancy? Highest life expectancy?

  SELECT name, lifeexpectancy, FROM country ORDER BY lifeexpectancy asc LIMIT 15;

  SELECT name, lifeexpectancy, FROM country WHERE lifeexpectancy > 0 ORDER BY lifeexpectancy desc LIMIT 15;



### Which five countries have the lowest population density? Highest population density?

  SELECT name, surfacearea, population FROM country WHERE population > 0 ORDER BY surfacearea / population asc LIMIT 5;

  SELECT name, surfacearea, population FROM country WHERE population > 0 ORDER BY surfacearea / population desc LIMIT 5;



### Which is the smallest country by area and population? the 10 smallest countries by area and population?

  SELECT name, surfacearea, population WHERE population > 0 ORDER BY surfacearea asc, population asc LIMIT 10;



### Which is the biggest country by area and population? the 10 biggest countries by area and population?

  SELECT name, surfacearea, population WHERE population > 0 ORDER BY surfacearea desc, population desc LIMIT 10;



# With section // WITH 'insertname' as (SELECT method)


### Of the smallest 10 countries, which has the biggest gnp?

  WITH smallest10 as (SELECT name, surfacearea FROM country ORDER BY surfacearea asc LIMIT 10)

  SELECT name, gnp FROM smallest10 ORDER BY gnp desc;



### Of the smallest 10 countries, which has the biggest per capita gnp?

  WITH smallest10 as (SELECT name, surfacearea, population FROM country WHERE population > 0 ORDER BY surfacearea asc LIMIT 10)

  SELECT name, gnp, population FROM smallest10 ORDER BY gnp / (surfacearea / population) desc;


### What is the sum of the surface area of the 10 biggest countries in the world? The 10 smallest?

  WITH sumbig10 as (SELECT surfacearea FROM country ORDER BY surfacearea desc LIMIT 10)
  SELECT SUM(surfacearea) FROM sumbig10;

  WITH sumlil10 as (SELECT surfacearea FROM country ORDER BY surfacearea asc LIMIT 10)
  SELECT SUM(surfacearea) FROM sumlil10;

# Group By // GROUP BY this

### How big are the continents in term or area and population?

  SELECT continent, SUM(surfacearea), SUM(population) FROM country GROUP BY continent;


### Which region has the highest average gnp?

  SELECT region, SUM(gnp) FROM country GROUP BY region ORDER BY SUM(gnp) desc LIMIT 1;


### Who is the most influential head of state measured by population?

  SELECT headofstate, SUM(population) FROM country WHERE headofstate != '' GROUP BY headofstate ORDER BY SUM(population) desc;


### Who is the most influential head of state measured by surface area?

  SELECT headofstate, SUM(surfacearea) FROM country WHERE headofstate != '' GROUP BY headofstate ORDER BY SUM(surfacearea) desc;


### What are the most common forms of government?

  SELECT COUNT(governmentform), governmentform FROM country GROUP BY governmentform ORDER BY COUNT(governmentform) desc;


### What are the forms of goverment for the top ten countries by surface area?

  WITH order10 as (SELECT surfacearea, governmentform FROM country ORDER BY surfacearea desc LIMIT 10)
  SELECT governmentform FROM order10 GROUP BY governmentform;


### What are the forms of government for the top ten richest nations?

  WITH caro10 as (SELECT gnp, governmentform FROM country ORDER BY gnp desc LIMIT 10)
  SELECT governmentform FROM caro10 GROUP BY governmentform;


### What are the forms of gorenment for the top ten richest per capita nations?

  WITH caro10 as (SELECT gnp, governmentform, population FROM country WHERE population > 0 ORDER BY (gnp / population) desc LIMIT 10)
  SELECT governmentform, gnp, population, name FROM caro10 GROUP BY governmentform, gnp, population, name;
