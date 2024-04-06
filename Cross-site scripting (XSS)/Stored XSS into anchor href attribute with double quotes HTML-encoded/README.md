## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f2dba6c5-a86f-4d90-bc6d-9d49208ba0a3)

## Solution :

We have a functionality to post comments.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fd2bd7f2-85ff-4acb-a504-b13d31c17f4a)

We can use the following XSS payload in the comment field to perform a stored Xss attack.

```js
javascript:alert()
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/837f50e9-a3d0-4390-a03c-6caade4d3f51)

Clicking the name above your comment should trigger an alert.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d8b6ea31-3ef4-4e99-9905-b1a8ec1a525a)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/25aa0394-9a28-4aed-90c7-044b9701b2a6)


