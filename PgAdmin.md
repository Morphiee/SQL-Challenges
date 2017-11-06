# Pg Admin 4 query's / Learn Challenge.

# Contributors

  - Morphiee
  - bkiahstroud

# Where Section // WHERE this = this

## What is the population of the US.

  SELECT name, population FROM country WHERE name = 'United States';

## What is the area of the US? (Surface Area)

  SELECT name, surfacearea FROM country WHERE surfacearea > 9000000;

## List countries in Africa that have a population smaller than 30,000,000 and a life expectency of more than 45.

  SELECT name, continent, population, lifeexpectancy FROM country WHERE population < 30000000 and continent = 'Africa' and lifeexpectancy > 45;

## What are countries that are like a republic?

  SELECT name, govermentform FROM country WHERE govermentform like '%Republic%';

## Which countries are some kind of republic and achieved their independence after 1945.

  SELECT name, indepyear, govermentform FROM country WHERE govermentform like '%republic%'' and indepyear > 1945;

## Which countries achieved independence after 1945 that are not some kind of republic?

  SELECT name, indepyear, govermentform FROM country WHERE govermentform not like '%republic%'' and indepyear > 1945;

# Oder by Section // ORDER BY this desc LIMIT #;

## Which fifteen countries have the lowest life expectancy? Highest life expectancy?

  SELECT name, lifeexpectancy, FROM country ORDER BY lifeexpectancy asc LIMIT 15;

  SELECT name, lifeexpectancy, FROM country WHERE lifeexpectancy > 0 ORDER BY lifeexpectancy desc LIMIT 15;

## Which five countries have the lowest population density? Highest population density?

  SELECT name, surfacearea, population FROM country WHERE population > 0 ORDER BY surfacearea / population asc LIMIT 5;

  SELECT name, surfacearea, population FROM country WHERE population > 0 ORDER BY surfacearea / population desc LIMIT 5;

## Which is the smallest country by area and population? the 10 smallest countries by area and population?

  SELECT name, surfacearea, population WHERE population > 0 ORDER BY surfacearea asc, population asc LIMIT 10;

## Which is the biggest country by area and population? the 10 biggest countries by area and population?

  SELECT name, surfacearea, population WHERE population > 0 ORDER BY surfacearea desc, population desc LIMIT 10;

# With section // WITH 'insertname' as (SELECT method)

## Of the smallest 10 countries, which has the biggest gnp?

  WITH smallest10 as (SELECT name, surfacearea FROM country ORDER BY surfacearea asc LIMIT 10)

  SELECT name, gnp FROM smallest10 ORDER BY gnp desc;

## Of the smallest 10 countries, which has the biggest per capita gnp?

  WITH smallest10 as (SELECT name, surfacearea, population FROM country WHERE population > 0 ORDER BY surfacearea asc LIMIT 10)

  SELECT name, gnp, population FROM smallest10 ORDER BY gnp / (surfacearea / population) desc;
