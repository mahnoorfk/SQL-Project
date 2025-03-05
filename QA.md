What are your risk areas? Identify and describe them.
-Accuracy of data 
As seen in the answer image of Q2 in 'starting_with_questions', the first row of the query states a city 'San Francisco' in country 'France'. This raises an issue of data accuracy. 


QA Process:
Describe your QA process and include the SQL queries used to execute it.

Changing data types: 

```
ALTER TABLE products
ALTER COLUMN orderedquantity TYPE integer USING (orderedquantity::int)
```
```
ALTER TABLE all_sessions
ALTER COLUMN totaltransacrev TYPE integer USING (totaltransacrev::int)
```
