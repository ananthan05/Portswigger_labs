## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fdcced1b-fdf7-4f8a-9307-48009bcaf641)

## Solution :

Visit a product, intercept the request in Burp Suite, and send it to Burp Repeater.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1751d2aa-e442-4d65-ace4-11b55f158637)

Go to the Repeater tab. Select the Referer header, right-click and select "Insert Collaborator Payload" to replace the original domain with a Burp Collaborator generated domain. Send the request.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fbcaa01c-03fc-4bf0-a102-0103a0198311)

After sending this request, the Burp Collaborator Client shows DNS and HTTP traffic from the lab, confirming that the server was coaxed to contact the provided external domain.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d8497aa2-d873-4c9d-b6e3-c2f687f18232)

At the same time, the lab page updates to lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bc87b976-efbb-48cc-b5a4-578924f9020c)
