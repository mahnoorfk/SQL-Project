**What are your risk areas? Identify and describe them.**

-The total transaction revenue in the all sessions table has a lot of null values. One way to improve the quality of the total transaction revenue data is to fill in the missing values. Looking at the analytics table, there is a unit price column and looking at the products table, there is an ordered quantity column. By joining all 3 tables and taking the sum of the unit price * ordered quantity, it may be possible to calculate total transaction revenue. Therefore, decreasing if not getting rid of all the null values. 

-When evaluating products that are in stock. It is unclear if the stock level data (in the all sessions table) has been updated after orders have been placed. The data shown may be the new stock levels. In that case the query for Q1 in the file 'starting_with_data' will be invalid. An alternative would be to just check if the stock level is greater than 0 in that case.

-The full visitor id and the visit id columns in the all sessions table have a lot of duplicate values. The all sessions table therefore does not have a primary key. 

-Verifying if data types have actually been changed 

-Accuracy of data as seen in the answer image of Q2 in the 'starting_with_questions' file, the first row of the query states a city 'San Francisco' in country 'France'. This raises an issue of data accuracy. 


**QA Process:**
**Describe your QA process and include the SQL queries used to execute it.**

**- Calculating the total transaction revenue using the data available in the products table (ordered quantity) and the analytics table (unit price):**

```
SELECT as.fullvisitorid, p.sku, SUM(a.unitprice*p.orderedquantity) AS total_revenue
FROM analytics a
JOIN all_sessions as USING (fullvisitorid)
JOIN products p
ON as.prodsku = p.sku
GROUP BY as.fullvisitorid, p.sku
```

**-Checking products in stock if the stock level data is updated after orders have been placed:**

```
SELECT sku, prodname, stocklevel
FROM products
WHERE stocklevel > 0
```

**Validating the data for unique values (full visitor id):**

```
SELECT fullvisitorid, COUNT(*)
FROM all_sessions
GROUP BY fullvisitorid
HAVING COUNT(*) > 1
```

**-Changing data types and then verifying if the column contains valid integer values:**

```
ALTER TABLE products
ALTER COLUMN orderedquantity TYPE integer USING (orderedquantity::int)
```

```
SELECT 
	CASE WHEN orderedquantity NOT BETWEEN 0 AND 999999 THEN NULL ELSE orderedquantity END) AS 	orderquant
FROM products
```


```
ALTER TABLE all_sessions
ALTER COLUMN totaltransacrev TYPE integer USING (totaltransacrev::int)
```

```
SELECT 
	CASE WHEN totaltransacrev NOT BETWEEN 0 AND 999999 THEN NULL ELSE totaltransacrev END) AS totalrev
FROM all_sessions
```

**-Checking data accuracy:**

```
SELECT a.country, a.city, AVG(p.orderedquantity) AS avg_ordered
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE city = 'San Francisco'
GROUP BY a.city, a.country
```