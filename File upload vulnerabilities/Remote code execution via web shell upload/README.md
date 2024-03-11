## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/84723d77-c841-4e29-bf0f-86adf257ebda)

## Solution : 

Log in to your account using the  credentials: `wiener:peter` 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6bdd96af-25a6-472f-9694-a94eeb00538a)

Notice the option for uploading an avatar image.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/063aa4bb-4b40-4f3b-aecb-2583c59c1d9e)

Upload an image.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c24e71d3-d716-44b6-b1e6-c7eb10bd774a)

Then return to your account page. Notice that a preview of your avatar is now displayed on the page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/32a61626-4e07-41cb-8833-77a87e4b9a04)

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

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e033efce-042a-489d-9383-eb72af0e1903)

The secret content is `ZEE6bXPToCA14LQAjFvkbjWsWtxIuvPn`

Now go to Home page and submit the solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1a0f2861-68b4-4b15-b01a-2e8ecec0d9ff)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/67d13919-e79e-4d4b-9bc2-9f762abb04eb)
