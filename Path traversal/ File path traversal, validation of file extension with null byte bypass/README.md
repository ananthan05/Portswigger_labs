## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5200961f-80ec-49c1-92ec-9d7caa19d1fd)

## Solution : 

An application may require the user-supplied filename to end with an expected file extension, such as .png. In this case, it might be possible to use a null byte to effectively terminate the file path before the required extension. 

For example: `filename=../../../etc/passwd%00.png`

Use Burp Suite to intercept and modify a request that fetches a product image.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/845110cc-c4e0-46b6-98d4-d944e10660e3)


Modify the filename parameter, giving it the value:

`../../../etc/passwd%00.jpg`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8d589c2d-414d-4aee-8d52-201691e03832)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/37b0f657-a327-47be-8ea0-d984def1408c)
