## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bdde755f-7846-4ee1-a4cf-c44e017ef90d)

## Solution :

Log in using the admin credentials.using `administrator:admin`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/97a98556-8af9-4aa8-8624-047a2515b372)

Browse to the admin panel, promote carlos, and send the HTTP request to Burp Repeater.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/74c60bbc-4054-4af0-9b0f-9a43bd4e75a1)

capture the request and send it top repeater .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/85af491a-5161-4bd7-8061-0f8dd63583b8)

We can see that in this POST request we have a parameter called username=carlos & action=upgrade
The above reqest upgrades the privileges of carlos user

and log in with the non-admin credentials `wiener:peter`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e2023ea3-3a48-4a78-8481-4a712ca15bb0)

Our goal is to exploit the flawed access controls to promote ourself (wiener) to become an administrator.

So we can try to perform the role changing action as wiener by pasting the cookie value of wiener in the request made by admin to change the privileges !

Cookie of admin - `FCo8YM39JByWk8Hg69oaWiRqioFpilKr` Cookie of wiener - `aHib8PgWpbrjRpK6Y9hTRmz9yy2PAE6`

So we change the cookie value of admin with wiener & send the request, we get the response as 401 - Unauthorized

Request -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/99e35507-06ea-4b1a-b0ef-944a991506ed)

Since this lab is based on Method-Based-Access control bypass, we can try to change the request from POST to GET. We can do this by Right click on request -> Click Change request method option.

Now it changes to a GET request-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/362d0107-a43c-4e7f-9be5-5b079d528f2f)

Lab solved. wiene become an admin.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/57ba573e-7cc6-48ef-82a3-9d06832780c2)

