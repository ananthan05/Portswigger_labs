## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8760639d-a0e4-44f9-ad01-099996273b20)

## Solution :

Log in to your account using the credentials: `wiener:peter`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/97e7899b-612e-4297-ab22-bb76a488405a)

Notice the option for uploading an avatar image.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/86aaeae3-e303-4cd9-9817-d1a63d0dacf9)

Upload an image.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c24e71d3-d716-44b6-b1e6-c7eb10bd774a)

Then return to your account page. Notice that a preview of your avatar is now displayed on the page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0c9a2ff6-a97d-4771-acbf-0e39b4e5a780)

In Burp, go to Proxy > HTTP history. Click the filter bar to open the Filter settings dialog. Under Filter by MIME type, enable the Images checkbox, then apply your changes.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e02076de-a1d9-4851-93c4-0fab6281f5fb)

In the proxy history, notice that your image was fetched using a GET request to /files/avatars/<YOUR-IMAGE> And one post request to /my-account/avatar also will be there . Send this two  request to Burp Repeater.

` /files/avatars/<YOUR-IMAGE>` 
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/65cbffb2-bf6b-4a01-a412-edaa99556322)


`/my-account/avatar`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7b58aa45-d266-4dad-b949-db8a1c2a8ca1)

Send this two  request to Burp Repeater.


In POST request `/my-account/avatar` we will remove the image content and change the file name and add a php script `<?php echo file_get_contents('/home/carlos/secret'); ?> `

orginal `/my-account/avatar` post request.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3cf18a9e-9fc3-4702-9d5c-8c03dcef6387)

After inserting the payload script and changing the file name to `exploit.php`.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a5b157fa-2f58-4360-a7c9-b218611c3c1a)

Now go to GET request ` /files/avatars/<YOUR-IMAGE>`  and change the file name to `exploit.php` and send.

Before changing the name the qurey was like this.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3736064b-beab-4fc7-9f1f-747d5709612f)

After  change the file name to `exploit.php` to see the secret content of the of folder in `/home/carlos/secret` with help of that php script  `<?php echo file_get_contents('/home/carlos/secret'); ?> `.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/eb3e89b5-4d40-4a3d-b899-408155ffad64)

The secret content is `asyUKxmWd7V9VxBdwszffYgsr1SDmldu `

Now go to Home page and submit the solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8f1c48cf-dcfd-4d24-88f3-0978d7e35e43)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e72267c5-84b6-4d0f-8829-236b6dbe8f2b)

