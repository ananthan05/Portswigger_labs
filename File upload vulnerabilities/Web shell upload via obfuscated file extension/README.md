## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/384538c8-25bc-417b-aa64-fd2e3ad4dfe7)

## Solution :

Log in and upload an image as your avatar, then go back to your account page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/96aedffe-1f74-4030-b379-2563863f79f4)


In Burp, go to Proxy > HTTP history. Click the filter bar to open the Filter settings dialog. Under Filter by MIME type, enable the Images checkbox, then apply your changes.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fb377783-7559-4f9f-9ca7-f598d53987f4)

In the proxy history, notice that your image was fetched using a GET request to `/files/avatars/<YOUR-IMAGE>` And one post request to `/my-account/avatar` also will be there . Send this two  request to Burp Repeater.

In POST request -
`/my-account/avatar` we will remove the image content and change the file name to `exploit.php` and add a php script `<?php echo file_get_contents('/home/carlos/secret'); ?> `

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/536458fc-0f67-40f0-84d8-712649a15bde)

 error came saying "Sorry, only JPG & PNG files are allowed".

 Change the value of the filename parameter to include a URL encoded null byte, followed by the .png extension:

`filename="exploit.php%00.png"`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0effb7af-78e6-4918-8dfe-221bab3427d4)

Send the request again and notice that the file was uploaded successfully.

In GET request-

Change the file name to exploit.php and send.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7b37c4c7-eb22-4f60-a2c9-f3c4dc4bf7b1)

The secret content is `QOdMt7gCd3sQtgfB1QQrxsqI9QXUH7wC`

Now go to Home page and submit the solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4c2382e0-76f3-465c-bc66-4fb2cb5a05f8)

LAB SOLVED.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/63106812-8450-4be3-94b4-c20ce638c1aa)


