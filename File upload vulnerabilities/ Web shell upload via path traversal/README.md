## Lab Description :


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3fc4c702-6157-4db2-b171-7cc279ebefbd)

## Solution :

Log in and upload an image as your avatar, then go back to your account page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3b59e77d-c5a5-47e3-b683-577e3f1deff2)

In Burp, go to Proxy > HTTP history. Click the filter bar to open the Filter settings dialog. Under Filter by MIME type, enable the Images checkbox, then apply your changes.


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fb377783-7559-4f9f-9ca7-f598d53987f4)

In the proxy history, notice that your image was fetched using a GET request to `/files/avatars/<YOUR-IMAGE>` And one post request to `/my-account/avatar` also will be there . Send this two  request to Burp Repeater.

In POST request `/my-account/avatar` we will remove the image content and change the file name to `exploit.php` and add a php script `<?php echo file_get_contents('/home/carlos/secret'); ?> `


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/685964cc-ed07-423a-ad7d-06ed6eb0c82b)


Now go to GET request  `/files/avatars/<YOUR-IMAGE>` and change the file name to exploit.php and send.


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9d52ac7e-6a0d-44e0-a7c4-4ea5f6a5f74c)

The php script  was displayed as plain text .  

By using file name as `../myexploit.php`

POST REQ-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a6e3328b-05df-4607-a63d-e8401527d9b0)

GET REQ-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9fa80d62-d621-4b53-bf0d-c6b817f1789d)

By using file name as `../myexploit.php` it can be noted that the server is stripping the directory traversal sequence but not  able retrive the data.

Obfuscate the directory traversal sequence by URL encoding the forward slash (/) character, resulting in:

`filename="..%2fexploit.php"`

POST REQ-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/50bf7281-e63a-4533-a85f-738da9121202)

GET REQ-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fbb8fc2b-1997-4f6f-9a76-7c118ba5ed78)

The secret content is `AV27jKwFf2ePRDuJVrXf3IKzBxTN80uk`

Now go to Home page and submit the solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e4083943-5b6a-4d5f-b4ea-cca07d76adb7)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/231f4043-235b-44ea-a674-9125b62d555a)




