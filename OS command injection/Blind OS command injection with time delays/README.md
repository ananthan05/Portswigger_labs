## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3bfc7cf7-9c38-482f-9ab5-f367f2b9aeb8)

## Solution : 

Use Burp Suite to intercept and modify the request that submits feedback.


Modify the email parameter, changing it to:

`email=x||ping+-c+10+127.0.0.1||`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/66f2b4d1-0537-4c6c-a3f8-675450728801)

Observe that the response takes 10 seconds to return

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4e5d0736-49dc-4e30-8af0-79f700cf6531)

LAB solved.
