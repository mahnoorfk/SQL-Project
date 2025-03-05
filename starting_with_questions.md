Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

```
SELECT city, country, SUM(totaltransacrev)
FROM all_sessions
WHERE totaltransacrev IS NOT NULL
GROUP BY city, country
ORDER BY SUM(totaltransacrev) DESC
```


Answer: 
Countries: United States, Israel, Canada, Australia, Switzerland

Cities: As seen in the image below

![Q1 Ans](https://github.com/user-attachments/assets/58a6532d-6ebb-41cc-9d16-8c8640022f14)

 

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

```
SELECT a.country, a.city, AVG(p.orderedquantity) AS avg_ordered
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
GROUP BY a.city, a.country
```


Answer:

![Q2 Ans](https://github.com/user-attachments/assets/72ff3cdc-ba22-482d-b6f4-d076063fc64d)



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

```
SELECT p.prodname, a.v2prodcategory, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'Canada' 
ORDER BY a.v2prodcategory
```
```
SELECT p.prodname, a.v2prodcategory, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'Canada' AND a.city = 'Vancouver'
ORDER BY a.v2prodcategory
```
```
SELECT p.prodname, a.v2prodcategory, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'Canada' AND a.city = 'Toronto'
ORDER BY a.v2prodcategory
```
```
SELECT p.prodname, a.v2prodcategory, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'United States' AND a.city = 'Los Angeles'
ORDER BY a.v2prodcategory
```
```
SELECT p.prodname, a.v2prodcategory, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'United Kingdom' AND a.city = 'London'
ORDER BY a.v2prodcategory
```


Answer: 
No patterns found. 

![Q3 Ans](https://github.com/user-attachments/assets/87d947ed-3f8c-44c9-927b-48187bab64b5)



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

```
WITH prodquantitybycountry AS 
(	SELECT a.country, p.prodname, SUM(p.orderedquantity) AS total_ordered
	FROM all_sessions a
	INNER JOIN products p
	ON a.prodsku = p.sku
	GROUP BY a.country, p.prodname
	ORDER BY total_ordered DESC
),

ranked AS 
(	SELECT *,
 	RANK() OVER (PARTITION BY country ORDER BY total_ordered DESC) AS rankedcountry
 FROM prodquantitybycountry
)

SELECT * 
FROM ranked
WHERE rankedcountry = 1
```


Answer: 
By scanning the data, it looks like 'Custom Decals' is a popular product in many countries such as Australia, Italy and South Korea. 

![image](https://github.com/user-attachments/assets/b3adb490-50f3-4cdb-b488-a5408c317874)



**Question 5: Can we summarize the impact of revenue generated from each city/country?**


SQL Queries:

```
SELECT country, city, SUM(totaltransacrev)
FROM all_sessions
WHERE totaltransacrev IS NOT NULL
GROUP BY country, city
```

Answer: 
It is difficult to create summaries of the total transaction revenue for each city/country as only 21 rows are returned for the above query out of 15,134 rows. That is 0.1% of data available. The total transaction revenue data is only available for 5 countries (United States, Israel, Canada, Australia, Switzerland). From the results, it is clear that United States has generated the highest amount of revenue and Switzerland has generated the least amount of of revenue. 
