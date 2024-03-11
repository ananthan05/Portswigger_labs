## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b2d0d120-04b5-4d4e-90e7-92d2b2a78afd)

## Solution : 

An application may require the user-supplied filename to start with the expected base folder, such as `/var/www/images`. In this case, it might be possible to include the required base folder followed by suitable traversal sequences.

For example: `filename=/var/www/images/../../../etc/passwd`

Use Burp Suite to intercept and modify a request that fetches a product image.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5738aaa6-60f1-4998-86f6-8392f827942e)

Modify the filename parameter, giving it the value:

`/var/www/images/../../../etc/passwd`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e514e420-f42e-4c96-a263-1bdabafdfbf4)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1447d906-7739-4965-845c-256df3a1c5c5)
