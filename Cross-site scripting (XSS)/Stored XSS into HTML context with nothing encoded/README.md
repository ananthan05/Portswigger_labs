## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5dfcc5a9-a4a8-4bcd-956b-d158bd857e77)

## Solution :

We have a functionality to post comments.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4fdbbf48-d98e-4731-b36b-bc9f1259e511)


We can use the following XSS payload in the comment field to perform a stored Xss attack.

```js
<script>alert(1)</script>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8f21964c-64fc-4589-aaa0-48e5a3f5aad1)

And post it.Lab Solved

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e49ac5aa-4f54-4057-8db8-52b66a0ab512)

Now each time when the page containing the comment is reloaded, it triggers an alert.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5b6b8d54-34b2-4f6c-91fa-3d528738f635)
