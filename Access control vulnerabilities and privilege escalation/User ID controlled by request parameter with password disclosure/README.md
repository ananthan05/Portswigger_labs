## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d124bdff-5c9f-4193-9ea7-5ba64b5b93ef)

## Solution :

Click on My Account , it takes us to login page. Use the credentials `wiener:peter` to login.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/01b40cb9-0cf5-4c89-ac07-d6877f534e92)

We can see there is a pre filled password in the password field. We can't see the password in plaintext but we can try reloading the page / view source-code to see what the password is.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c4b377ea-b6b5-499f-aa76-9da9f496a61f)

So the password is prefilled with the password of the user winer which we logged in.

Now send this repeater and Change the parameter ?id=wiener to ?id=administrator.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/769baa93-5cbc-47e8-90df-a769a3606ebe)

Thus we have sucessfully exploited it as it leaked the admin's password in the response.

Password - `26leg2i40urap1xbkhto`

Now go and  login as admin. 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/59b21fca-483a-45af-bd83-f4ebc85f9330)

delete user carlos to solve the lab.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ae6f3519-ec37-448f-9e6b-1429609a52aa)
