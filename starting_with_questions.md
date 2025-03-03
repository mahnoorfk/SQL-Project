Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT *
FROM all_sessions
WHERE transacrevenue IS NOT NULL
ORDER BY transacrevenue DESC


Answer: Country: USA
	City: Only Sunnyvale is stated  




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT AVG(p.orderedquantity), a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
GROUP BY a.city, a.country


Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT a.v2prodcategory, p.prodname, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'Canada' AND a.city = 'Vancouver'
ORDER BY a.v2prodcategory

SELECT a.v2prodcategory, p.prodname, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'Canada' AND a.city = 'Toronto'
ORDER BY a.v2prodcategory

SELECT a.v2prodcategory, p.prodname, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'United States' AND a.city = 'Los Angeles'
ORDER BY a.v2prodcategory

SELECT a.v2prodcategory, p.prodname, a.city, a.country
FROM all_sessions a
INNER JOIN products p
ON a.prodsku = p.sku 
WHERE a.country = 'United Kingdom' AND a.city = 'London'
ORDER BY a.v2prodcategory


Answer: No patterns found





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







