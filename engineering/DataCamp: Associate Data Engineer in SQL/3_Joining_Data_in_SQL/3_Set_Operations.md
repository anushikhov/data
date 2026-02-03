## Set Operations  

SQL has three main set operations: UNION, INTERSECT, EXCEPT.  

## UNION  

**UNION takes two tables as input, and returns all records from both tables, removing duplicates.**  

**UNION ALL takes two tables and returns all records from both tables, including duplicates.**  

```  
SELECT *  
FROM left_table  
UNION  
SELECT *  
FROM right_table;  
```  

```  
SELECT *  
FROM left_table  
UNION ALL  
SELECT *  
FROM right_table;  
```  

```  
SELECT monarch AS leader, country  
FROM monarchs  
UNION ALL  
SELECT prime_minister, country  
FROM prime_ministers  
ORDER BY leader, country  
LIMIT 10;  
```  

**UNION query must have the same number of columns.**  

**Both queries on the left and right of the set operation must have the same data types. The names of the fields do not need to be the same, as the result will always contain field names from the left query.**  

Perform a set operation to stack all records in economies2015 and economies2019 on top of each other, excluding duplicates.  

```  
SELECT * FROM economies2015  
UNION  
SELECT * FROM economies2019  
ORDER BY code, year;  
```  


Perform an appropriate set operation that determines all pairs of country code and year (in that order) from _economies_ and _populations_, excluding duplicates. Order by country code and year.  

```  
-- Query that determines all pairs of code and year from economies and populations, without duplicates  
SELECT code, year FROM economies  
UNION  
SELECT country_code, year FROM populations  
ORDER BY code, year;  
```  

Amend the query to return all combinations (including duplicates) of country _code_ and _year_ in the _economies_ or the _populations_ tables.  

```  
SELECT code, year  
FROM economies  
UNION ALL  
SELECT country_code, year  
FROM populations  
ORDER BY code, year;  
```  

## INTERSECT  
  
**INTERSECT takes two tables as input, and returns only the records that exist in both tables.**  

The syntax for this set operation is similar to that of UNION and UNION ALL. We perform a SELECT statement on the first table, a SELECT statement on the second table, and specify the set operator between them.  


