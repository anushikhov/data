## Outer Joins, Cross Joins and Self Joins  

**LEFT JOIN will return all records in the left table, and those records in the right table that match on the joining field provided.**    
  

**left table**  

| id            | left\_val     |
| ------------- |:-------------:|
| 1             | L1            |
| 2             | L2            |
| 3             | L3            |  
| 4             | L4            |  

**right table**  

| id    | right\_val |
|-------|:----------:|
| 1     | R1         |
| 4     | R2         |
| 5     | R3         |
| 6     | R4         |


**result after LEFT JOIN**  

| id  | left\_val | right\_val |
|-----|:---------:|:-----------|
| 1   | L1        | R1         |
| 2   | L2        | L2         |
| 3   | L3        | null       |
| 4   | L4        | null       |  


```  
SELECT p1.country, prime_minister, president  
FROM prime_ministers AS p1  
LEFT JOIN presidents AS p2  
USING(country);  
```  

**LEFT JOIN can also be written as LEFT OUTER JOIN.**  

## RIGHT JOIN syntax  

```  
SELECT *  
FROM left_table  
RIGHT JOIN right_table  
ON left_table.id = right_table.id;  
```  

**RIGHT JOIN can also be written as RIGHT OUTER JOIN in SQL.**  

**RIGHT JOIN is less commonly used than LEFT JOIN because any RIGHT JOIN can be re-written as a LEFT JOIN.**  

*Because we typically write from left to right, LEFT JOIN feels more intuitive to users when typing from left to right.*  

--------------------------------------------------------------------------------------------------  
*To become faster at writing queries, it's helpful to memorize their structure.*  

```  
SELECT c.name AS country, local_name, l.name AS language, percent  
FROM countires AS c  
LEFT JOIN languages AS l  
USING(code)  
ORDER BY country DESC;  
```  

You'll explore the differences between INNER JOIN and LEFT JOIN. This will help you decide which type of join to use.  You'll be using the *cities* and *countries* tables.  

You'll begin with an *INNER JOIN* with the *cities* table (left) and *countries* table (right). **This helps if you are interested only in records where a country is present in both tables.**  

You'll then change to a *LEFT JOIN*. This helps if you're interested in returning all countries in the *cities* table, whether or not they have a match in the *countries* table.  

Perform an inner join with *cities AS c1* on the left and *countries AS c2* on the right. Use *code* as the field to merge your tables on.  

```  
SELECT c1.name AS city,  
       code,   
        c2.name AS country,  
        region,  
        city_proper_pop  
FROM cities AS c1  
INNER JOIN countries AS c2  
ON c1.country_code = c2.code  
ORDER BY code DESC;  
```  

Change the code to perform a LEFT JOIN instead of an INNER JOIN.  

```  
SELECT c1.name AS city,  
       code,   
        c2.name AS country,  
        region,  
        city_proper_pop  
FROM cities AS c1  
INNER JOIN countries AS c2  
ON c1.country_code = c2.code  
ORDER BY code DESC;  
```  
*Remember that the LEFT JOIN is a type of outer join: its result is not limited to only those records that have matches for both tables on the joining field.*  

------------------------------------------------------------------------------------------------  

Use the AVG() function with a LEFT JOIN to determine the average gross domestic product (GDP) per capita by region in 2010.  

Complete the LEFT JOIN with the countries table on the left and the economies table on the right on the code field.  
Filer the records fromt he year 2010.  

```  
SELECT name, region, gdp_percapita  
FROM countries AS c  
LEFT JOIN economies AS e  
USING(code)  
WHERE year = 2010;  
```   

To calculate per capita GDP per region, begin by grouping by *region*.  

After your *GROUP BY*, choose *region* in your *SELECT* statement, followed by average GDP per capita using the *AVG()* function, with *AS avg_gdp* as your alias.  

```  
-- Select region, and average gdp_percapita as avg_gdp  
SELECT region, AVG(gdp_percapita) AS avg_gdp  
FROM countries AS c  
LEFT JOIN economies AS e  
USING(code)  
WHERE year = 2010  
-- Group by region  
GROUP BY region;   
```   

Order the result set by the average GDP per capita from highest to lowest.  
Return only the first 10 records in your result.  

```  
SELECT region, AVG(gdp_percapita) AS avg_gdp  
FROM countries AS c  
LEFT JOIN economies AS e  
USING(code)  
WHERE year = 2010  
GROUP BY region  
-- Order by descending avg_gdp  
ORDER BY avg_gdp DESC  
-- Return only first 10 records  
LIMIT 10;  
```  

It can be tricky to wrap one's head around when left and right joins return equivalent results.  

Write a new query using *RIGHT JOIN* that produces an identical result to the *LEFT JOIN* provided.  

```  
-- Modify this query to use RIGHT JOIN instead of LEFT JOIN  
SELECT countries.name AS country,   
       languages.name AS language,  
       percent  
FROM countries  
LEFT JOIN languages  
USING(code)  
ORDER BY language;  
```  

```  
SELECT countries.name AS country,  
       languages.name AS language,  
       percent   
FROM languages  
RIGHT JOIN countries  
USING(CODE)  
ORDER BY language;  
```  

**When converting a LEFT JOIN to a RIGHT JOIN, change both the type of join and the order of the tables to get equivalent results. The order of the fields you are joining ON still doesn't matter.**  



## FULL JOINs  

**A FULL JOIN combines a LEFT JOIN and a RIGHT JOIN.**  

```  
SELECT left_table.id AS L_id,  
       right_table.id AS R_id,  
       left_table.val AS L_val,  
       right_table.val AS R_val  
FROM left_table  
FULL JOIN right_table  
USING(id);  
```  

*The keyword FULL OUTER JOIN can also be used.*  

```  
SELECT p1.country AS country, prime_minister, president  
FROM prime_ministers AS p1  
FULL JOIN presidents AS p2  
ON p1.country = p2.country  
LIMIT 10;  
```  

## Chaining FULL JOINs  

Suppose you are doing some research on Melanesia and Micronesia, and are interested in pulling information about languages and currencies into the data we see for these regions in the *countries* table. Since languages and currencies exist in separate tables, this will require two consecutive full joins involving the *countries*, *languages*, and *currencies* tables.  

Complete the *FULL JOIN* with *countries as c1* on the left and *languages as l* on the right, using *code* to perform the join.  
Next, chain this join with another *FULL JOIN*, placing *currencies* on the right, joining on *code* again.  


```  
SELECT c1.name AS country,  
       region,  
       l.name AS language,  
       basic_unit,  
       frac_unit  
FROM countries AS c1  
FULL JOIN languages AS l  
USING(code)  
FULL JOIN currencies AS c2  
USING(code)  
WHERE region LIKE 'M&esia';  
```  

## CROSS JOINS  

*CROSS JOINS* create all possible combinations of two tables.  

```  
SELECT id1, id2  
FROM table1  
CROSS JOIN table2;  
```  

Pairing prime ministers with presidents  

```  
SELECT prime_minister, president  
FROM prime_ministers AS p1  
CROSS JOIN presidents AS p2  
WHERE p1.continent IN ('Asia')  
AND p2.continent IN ('South America');  
```  

**CROSS JOIN can be incredibly helpful when asking questions that involve looking at all possible combinations or pairings between two sets of data.**  

Imagine you are a researcher interested in the languages spoken in two countries: Pakistan and India. You are interested in asking:  

1. What are the languages presently spoken in the two countries?  
2. Given the shared history between the two countries, what languages could potentially have been spoken in either country over the course of their history?  

Complete the code to perform an INNER JOIN of *countries AS c* with *languages AS l* using the *code* field to obtain the languages currently spoken in the two countries.  

```  
SELECT c.name AS country, l.name AS language  
FROM countries AS c  
INNER JOIN languages AS l  
USING(code)  
WHERE c.code IN ('PAK','IND')  
AND l.code IN ('PAK','IND');  
```  
Change your *INNER JOIN* to a different kind of join to look at possible combinations of languages that could have been spoken in the two countries given their history.  

```  
SELECT c.name AS country, l.name AS language  
FROM countries AS c  
CROSS JOIN languages AS l  
WHERE c.code IN ('PAK','IND')  
AND l.code IN ('PAK','IND');  
```  

---------------------------------------------------------------------------  
Determine the names of the five countries and their respective regions with the lowest life expectancy for the year 2010.  

* Complete the join of *countries AS c* with *population AS p*.  
* Filter on the year 2010.  
* Sort your results by life expectancy in ascending order.  
* Limit the result to five countries.  

```  
SELECT  
   c.name AS country,  
   region,  
   life_expectancy AS life_exp  
FROM countries AS c  
-- Join to populations (alias as p) using an appropriate join  
INNER JOIN populations AS p  
ON c.code = p.country_code  
-- Filter for only results in the year 2010  
WHERE year = 2010
-- Sort by life_exp  
ORDER BY life_exp 
-- Limit to five records  
LIMIT 5;  
```  

*All four types of joins will return the same result.*  

## Self joins  

Self joins can be used to compare parts of the same table.  

**Aliasing is required for a self join.**  

```  
SELECT  
  p1.country AS country1,  
  p2.country AS country2,  
  p1.continent  
FROM prime_ministers AS p1  
INNER JOIN prime_ministers AS p2  
ON p1.continent = p2.continent  
  AND p1.country <> p2.country   
LIMIT 10;  
```  

Comparing a country to itself  

Self joins are very useful when comparing data from one part of a table with another part of the same table.  

Suppose you are interested in finding out how much the populations for each country changed from 2010 to 2015. You can visualize this change by performing a self join.  

Perform an inner join of *populations* with itself *ON* _country\_code_, aliased _p1_ and _p2_ respectively.  

Select the _country\_code_ from _p1_ and the _size_ field from both _p1_ and _p2_, aliasing _p1.size_ as _size2010_ and _p2.size_ as _size2015_ (in that order).  

```  
SELECT p1.country_code,   
       p1.size AS size2010,  
       p2.size AS size2015   
FROM populations AS p1  
INNER JOIN populations AS p2  
ON p1.country_code = p2.country_code;  
```  

Since you want to compare records from 2010 and 2015, eliminate unwanted records by extending the _WHERE_ statement to include only records where the _p1.year_ matches _p2.year - 5_.  

```  
SELECT  p1.country_code,  
        p1.size AS size2010,  
        p2.size AS size2015  
FROM populations AS p1  
INNER JOIN populations AS p2  
ON p1.country_code = p2.country_code  
WHERE p1.year = 2010  
-- Filter such that p1.year is always five years before p2.year  
AND p1.year = p2.year - 5;  
```   

Match  

INNER JOIN - You sell houses an have two tables, _listing\_prices_ and _price\_sold_. You want a table with sale prices and listing prices, only if you know both.   

LEFT JOIN - You run a pizza delivery service with local clients. You want a table of clients and their weekly orders, with nulls if there are no orders.  

FULL JOIN - You want a report of whether your patients have reached out to you, or you have reached out to them. You are fine with nulls for eiter condition.  







