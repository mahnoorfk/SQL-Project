What issues will you address by cleaning the data?

**-Getting rid of incorrect values**

**-Getting rid of null values** 

**-Checking for duplicates**


Queries:
Below, provide the SQL queries you used to clean your data.

**-Getting rid of incorrect values:**

```
SELECT *
FROM all_sessions
WHERE city NOT LIKE '%not%'
```
```
SELECT *
FROM all_sessions
WHERE country NOT LIKE '%not%'
```
```
SELECT *
FROM all_sessions
WHERE v2prodcategory NOT LIKE '%not%'
```
**-Getting rid of null values:**

```
SELECT *
FROM all_sessions
WHERE totaltransacrev IS NOT NULL
```
```
SELECT *
FROM all_sessions
WHERE city IS NOT NULL
```
```
SELECT *
FROM all_sessions
WHERE country IS NOT NULL
```
**-Checking for duplicates:** 

```
SELECT fullvisitorid, COUNT(*)
FROM all_sessions
GROUP BY fullvisitorid
HAVING COUNT(*) > 1
```
```
SELECT sku, COUNT(*)
FROM products
GROUP BY sku
HAVING COUNT(*) > 1
```
