## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/544be3ed-0756-4544-99ad-795f184d3877)


## Solution :
Log in using the supplied credentials and access your account page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/414d9203-c844-4cbf-8aed-b2a42f786cf5)

And provided feature to update the email address associated with your account

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7fdf5293-05b0-4b44-aec1-12daab9f3b17)

Observe that the response contains your role ID.ie in the `post request` 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1d948e21-3d8b-4ddd-96c5-968f926e6e40)

Send the email submission request to Burp Repeater. And add "roleid":2 to the email parameterand send.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2ca6c9c7-9e3a-40d4-9e6d-08152f0e4480)

Then go to the page and refresh it.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7db97071-4ef3-43a6-aebc-aa89b425bfab)

admin panel is visible now go there and delete carlos .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/de55f383-6b2e-4804-9fc1-e56c6a40a9fa)

Lab solved.

