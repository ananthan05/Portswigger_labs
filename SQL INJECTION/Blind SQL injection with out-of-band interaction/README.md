## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0c8f9c66-4a4e-4986-809c-7f98925ddf02)

## Solution :

The payloads for each domain to perform a DNS lookup to an external domain.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/568c42f2-93d8-4a55-8fa9-ad774eeef678)

Query made - 

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'
```

Since we are unsure of the database we are working with, we attempt every payload listed on DNS lookup for every database.

Request captured -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/81437c77-9b98-4f97-9b02-43793a3f4d91)

`Send this to Repeater`
