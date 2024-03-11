## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4a340dcc-5c55-41b4-a4e7-fc2b5ca139c9)

## Solution :

When the exploit PHP code was attempted to be uploaded, the server refused access, claiming it was not an image file.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/55c8172d-4f0f-4f64-a75a-1263e586bf32)

Create a polyglot PHP/JPG file that is fundamentally a normal image, but contains your PHP payload in its metadata using exiftoolwith this command

`exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" <YOUR-INPUT-IMAGE>.png -o polyglot.php`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5b481b6b-eff4-4727-ac14-1697e6d894e0)

This adds your PHP payload to the image's Comment field, then saves the image with a .php extension.

In the browser, upload the polyglot image as your avatar,

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4ec61396-ccf8-4f8e-aea7-7392c0608963)

Then go back to your account page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f08ac740-b86e-4644-b963-e92104464dbd)

In Burp's proxy history, find the GET /files/avatars/polyglot.php request.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/62878fa7-87f5-4ff4-9c90-ff108f6dfb26)

Use the message editor's search feature to find the START string somewhere within the binary image data in the response. Between this and the END string, you should see Carlos's secret.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/627dcaf4-ebb9-4eb8-b03a-e8d0f4d5af9a)

The secret content is `G5n3uPAmgQQKbqFf0YBIrsARz5vzJ0nr`

Now go to Home page and submit the solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/305c9de7-abd1-4486-ba49-8672e750a466)

LAB SOLVED.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/03809a5e-1072-4816-95fc-eab94d66fa21)

