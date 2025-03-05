**Question 1: List the ordered product names that are not in stock**

SQL Queries:

```
SELECT sku, prodname
FROM products
WHERE orderedquantity > stocklevel
```

Answer: 

![OwnQ1](https://github.com/user-attachments/assets/aead4bc0-0248-42a4-aa7f-8df717ea38f3)



**Question 2: List the unique product prices**

SQL Queries:

```
SELECT DISTINCT(prodprice)
FROM all_sessions
```

Answer:

![OwnQ2](https://github.com/user-attachments/assets/b94bce6e-05ea-4019-af5d-ebeb1acbb454)



**Question 3: To help analyze website traffic patterns, return the list of unique countries who's website traffic source is 'Paid Search'**

SQL Queries:

```
SELECT DISTINCT(country), channelgrouping
FROM all_sessions
WHERE channelgrouping = 'Paid Search'
```

Answer:

![OwnQ3](https://github.com/user-attachments/assets/87e870fc-29b4-4465-ba65-1c5ab58a2580)


Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
