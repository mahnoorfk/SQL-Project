What issues will you address by cleaning the data?
Get rid of nulls 





Queries:
Below, provide the SQL queries you used to clean your data.

--Checking for duplicates for fullvisitorid(primary key):

SELECT fullvisitorid, COUNT(*)
FROM all_sessions
GROUP BY fullvisitorid
HAVING COUNT(*) > 1



--Checking for duplicates for sku(primary key):

SELECT sku, COUNT(*)
FROM products
GROUP BY sku
HAVING COUNT(*) > 1

**NO DUPLICATES FOUND**

--Q1: CLEANING 

-SELECT *
FROM all_sessions
WHERE transacrevenue IS NOT NULL

transactionrevenue is too high, maybe divide by 1M
Change data type for transacrevenue
Checked for null country and city but there is none 
Change data type from text to varchar(30)?

--Q2: change data type of ordered quantity
checked for nulls but none




What to put in QA: finding answer doing another method to get answer 
% of null in table with 15k rows
Hey wait I can get transaction revenue with unit price and quantity

ERD: Productsku is prmary key in products and can be foreign key in other tables, otherwise the other tables cant be connected  
Set up constraint in products table with sku as primary key 