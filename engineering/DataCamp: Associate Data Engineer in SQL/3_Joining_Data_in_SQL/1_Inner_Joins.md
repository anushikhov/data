## INNER JOINS  

**A key is a single column or a group of columns that uniquely identifies a record in a table.**  

**INNER JOIN looks for records in both tables which match on a given field.**  

```    
SELECT *   
FROM presidents;  
```   

```  
--Inner join of presidents and prime_ministers, joining on country   
SELECT prime_ministers.country, prime_ministers.continent, prime_minister, president   
FROM presidents   
INNER JOIN prime_ministers   
ON presidents.country = prime_ministers.country;  
```   

Note. the table.column\_name format must be used when selecting columns that exist in both tables to avoid a SQL error.   

**Aliases can be used in the table.column_name syntax in SELECT and ON clauses.**  

```   
--Inner join of presidents and prime_ministers, joining on country   
SELECT p2.country, p2.continent, prime_minister, president  
FROM presidents AS p1  
INNER JOIN prime_ministers AS p2  
ON p1.country = p2.country;  
```   

**When joining on two identical column name, we can employ the USING command followed by the shared column name in parentheses.**  

```  
--Inner join of presidents and prime_ministers, joining on country  
SELECT p2.country, p2.continent, prime_minister, president  
FROM presidents AS p1  
INNER JOIN prime_ministers AS p2  
USING(country);  
```  

Use the cities and countries tables to build the inner join.  
1. Start off by selecting all columns   
2. Perform the inner join   
3. Refine the join to a specific columns  

Begin by selecting all columns from the cities table, using the SQL shortcut that selects all.  

```  
-- Select all columns from cities  
SELECT *  
FROM cities;  
```  

**Table aliases are helpful in allowing you to reference them in other parts of your query, like the SELECT statement.**  

**When writing joins, many SQL users prefer to write the SELECT statement after writing the join code, in case the SELECT statement requires using table aliases.**  

Join the tables _countries AS c_ with _economies AS e_.  
Use _code_ as your joining field; do not use the _USING_ command here.  
Select the following columns in order: _code_ from the _countries_ table (aliased as _country_code_), _name_, _year_, and _inflation_rate_.  

```  
SELECT c.code AS country_code, name, year, inflation_rate   
FROM countries AS c   
INNER JOIN economies AS e  
ON c.code = e.code;   
```   

**When both the field names being joined on are the same, you can take advantage of the USING clause.**  

```  
SELECT c.name AS country, l.name AS language, official  
FROM countries AS c  
INNER JOIN languages AS l  
USING(code);  
```  

## Defining relationships  

The types of relationships that can exist between tables:  
* One-to-many  
* One-to-one  
* Many-to-many  

The _countries_ table has a many-to-many relationship with the _languages_ table. That is, many languages can be spoken in a country, and a language can be spoken in many contries.  

What is the best way to query all the different languages spoken in a country? Or, all the countries that speak a certain language?  

Select the country _name_, aliased as _country_, from the _countries_ table.  

```  
SELECT name AS country  
FROM countries;  
```   

Add an alias _c_ for the _countries_ table and perform an inner join with the _language_ table, _l_, on the right; join on _code_ in line 8 with the _USING_ keyword; include the language name, aliased as _language_.  

```   
SELECT c.name AS country, l.name AS language  
FROM countries AS c  
INNER JOIN languages AS l  
USING(code);   
```   

Add a _WHERE_ clause to find out how many contries speak the language 'Bhojpuri'.  

```  
SELECT c.name AS country, l.name AS language  
FROM countries AS c  
INNER JOIN languages AS l  
USING(code)  
WHERE l.name = 'Bhojpuri';   
```   

## Joins on joins  

```  
SELECT *  
FROM left_table  
INNER JOIN right_table  
ON left_table.id = right_table.id  
INNER JOIN another_table  
ON left_table.id = another_table.id;  
```  

```  
SELECT p1.country, p1.continent,  
       president, prime_minister  
FROM prime_ministers AS p1  
INNER JOIN presidents AS p2  
USING(country);  
```   

## Chaining joins  

```  
-- SQL query for chaining inner joins  
SELECT  
   p1.country,  
   p1.continent,  
   president,  
   prime_minister,  
   pm_start  
FROM prime_ministers AS p1  
INNER JOIN presidents AS p2  
USING(country)  
INNER JOIN prime_minister_terms AS p3  
USING(prime_minister);  
```  

## Joining on multiple keys  

It isn't always the case that each value in the field being joined on corresponds to exactly one record in the joining field of the right table.  

We can limit the records returned by supplying an additional field to join on by adding the AND keyword to our ON clause.  

In this example, we join on date, a frequently used second column when joining on multiple fields. The result set now contains records that match on both id AND date.  

```  
SELECT *  
FROM left_table  
INNER JOIN right_table  
ON left_table.id = right_table.id  
  AND left_table.date = right_table.date;  
```   

Suppose you are interested in the relationship between fertility and unemployment rates. Your task in this exercise is to join tables to return the country name, year fertility rate, and unemployment rate in a single result from the _countries_, _populations_ and _economies_ tables.  

Do an inner join of _countries AS c_ (left) with _populations AS p_ (right), on _code_. Select _name_ and _fertility_rate_.  

```   
SELECT name, fertility\_rate 
FROM countries AS c  
INNER JOIN populations AS p  
ON c.code = p.country_code;  
```  

Chain an inner join with the _economies_ table _AS e_, on _code_.  
Select _year_ and _unemployment_rate_ from the _economies_ table.  

```  
SELECT name, e.year, fertility\_rate, unemployment_rate
FROM countries AS c  
INNER JOIN populations AS p  
ON c.code = p.country_code  
INNER JOIN economies AS e  
ON p.country_code = e.code;  
```   

## Checking multi-table joins  

You can see that the 2015 _fertility\_rate_ has been paired with 2010 _unemployment\_rate_ and vice versa.  

Instead of four records, the query should return two: one for each year. The last join was performed on _c.code = e.code_, without also joining on _year_.  

Fix the query by explicitly stating that both the country _code_ and _year_ should match!  

```  
SELECT name, e.year, fertility_rate, unemployment_rate  
FROM countries AS c  
INNER JOIN populations AS p  
ON c.code = p.country_code  
INNER JOIN economies AS e  
ON c.code = e.code  
AND p.year = e.year;  
```  




