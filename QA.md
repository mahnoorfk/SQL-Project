What are your risk areas? Identify and describe them.



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
