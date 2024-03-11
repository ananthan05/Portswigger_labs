## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2c16020b-c84f-4a3a-b9d8-dbc2f159766d)

## Solution :

Log in and upload an image as your avatar, then go back to your account page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/62dae6b3-11db-4261-935e-a59b05da98ef)


In Burp, go to Proxy > HTTP history. Click the filter bar to open the Filter settings dialog. Under Filter by MIME type, enable the Images checkbox, then apply your changes.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fb377783-7559-4f9f-9ca7-f598d53987f4)

In the proxy history, notice that your image was fetched using a GET request to `/files/avatars/<YOUR-IMAGE>` And one post request to `/my-account/avatar` also will be there . Send this two  request to Burp Repeater.

In POST request -
`/my-account/avatar` we will remove the image content and change the file name to `exploit.php` and add a php script `<?php echo file_get_contents('/home/carlos/secret'); ?> `

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/19577420-e884-418e-8b89-6a89e79bc14c)

But now in post request it is saying it php files are not allowed.

So we will be  changing the value of the filename parameter to `.htaccess`.

Change the value of the Content-Type header to `text/plain`. ANd Replace the contents of the file (your PHP payload) with the following Apache directive:

`AddType application/x-httpd-php .shell`

`This maps an arbitrary extension (.shell) to the executable MIME type application/x-httpd-php. As the server uses the mod_php module, it knows how to handle this already.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1100ae23-3a12-4c79-9f0b-4f0a3a906f64)


Use the back arrow in Burp Repeater to return to the original request for uploading your PHP exploit.And Change the value of the filename parameter from exploit.php to exploit.shell then 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bdb53fe3-6a00-4525-a72b-5d783fcf8731)

Send the request again and notice that the file was uploaded successfully.

In GET request-

Change the file name to exploit.shell and send.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/55b551fd-2807-4337-be71-5a2be240e327)

The secret content is `UcRHHEgBn5QswMYfn6StQHU4x4ISeism`

Now go to Home page and submit the solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/40cf4af0-193b-413b-826a-3b9087a4947e)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a774871f-1253-4ae0-af13-5718d2260460)


