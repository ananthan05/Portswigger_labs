## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/dea0ba06-b9ec-4398-96a5-19fab3190876)

## Solution :

Click on My Account , it takes us to login page. Use the credentials `wiener:peter` to login.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/af7fa1bc-9c63-4f1b-ac3c-6bbeec8213c4)

Send the request to repeater tab. Change the value to ?id=carlos and observe the response.

We get a 302 Redirect response back .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2d017d76-6c91-42f1-9d61-f1ff29a64ea1)

but  the API key of Carlos is leaked in the redirect response.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/410286e4-0d5a-4d04-bf32-e302ddb52612)

`In some cases, an application does detect when the user is not permitted to access the resource, and returns a redirect to the login page. However, the response containing the redirect might still include some sensitive data belonging to the targeted user, so the attack is still successful.`

API key of carlos `01SODvIgS7xYBqFUAHupxfHo3i5JX1yP`

Go to home page and submit it.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7486c7be-2c54-420d-bbe4-b6da9723fccc)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b104bae8-3eeb-42b7-94fc-be615efc1acb)

