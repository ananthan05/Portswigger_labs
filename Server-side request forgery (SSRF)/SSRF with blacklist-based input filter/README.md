## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c2ed66db-c788-4ccc-baa1-7f033a82fe4b)

## Solution :

Visit a product, click "Check stock", intercept the request in Burp Suite, and send it to Burp Repeater.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/af6e142c-05f3-4ef4-bc38-10a6c835c250)

Change the URL in the stockApi parameter to `http://127.0.0.1/` and observe that the request is blocked.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3f41a489-c11e-487e-9d0b-be7319b1237e)

Bypass the block by changing the URL to: `http://127.1/`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/622cfec8-07ec-41db-a952-b55bdc42a3e3)

Change the URL to `http://127.1/admin` and observe that the URL is blocked again.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/61834cdb-bf75-49e3-98fa-379cf382c004)

Obfuscate the "a" by double-URL encoding it .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f5dc8eb8-0d8f-40e1-acb9-f18f0fd6fa16)

by doing this twice it will  double-URL encoded.

Result-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0a2c4d5f-ca8b-42f4-910f-196646b8a0fa)

Now delete carlos . 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f7b22456-27ae-410a-bb9b-16cc98b47726)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/66286b52-bec4-4539-81d0-be667972282f)

