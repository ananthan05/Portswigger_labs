## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f4f7115e-958d-4e66-a265-fa605fece86a)

## Solution :

On your system, create a file called `exploit.php` containing a script for fetching the contents of Carlos's secret.

For example:`<?php echo file_get_contents('/home/carlos/secret'); ?>`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e35273c6-b0f3-4fe6-a06c-f1daaa2d8370)

Log in and attempt to upload the script as your avatar.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/19763f82-6a93-4621-a76c-da049c5ed595)

 Observe that the server appears to successfully prevent you from uploading files that aren't images.

 ![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b4657528-7590-4e3d-b4af-f0b716c57a84)


Now what we need to do is we will a time gap between checking the file and unlinking the file.we need to find that gap and extract the content from that.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/25e40e77-04c2-4bf6-83d8-d9c2335eca68)

For that go http history and the `post request` that we tried to upload the file and send this to the repeter.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/81e8f120-331b-4e98-b007-9e67e142db58)

simlary find any `Get request`  and give the file directory as `/files/avatars/exploit.php` this because it should give the content.

sended this get reqest.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5a58a834-83af-4dc7-882e-74b6ca3c004e)

and change the file directory as `/files/avatars/exploit.php`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6e3c1869-25e9-449b-ba85-9de79d73263a)

There is only a small time gap between the checking the file and unlinking the file and we need excute is simultaneously and we need to duplicate some get request in repeter beacuse some will have the chances of failure becuse of the small time gap.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/58e866a7-56e0-48ee-b75e-379f5c1547a5)

Now 1 post request and 8 get request(of same content) are there. so what we are doing here we are uploading one time abd calling serveral time in that time gap.we dont know one reqest may come or other won't .

we need excute is all this reqest simultaneously . So for that  click on new tab option in the repeater from that click on `create tab group`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/83a084ce-038f-4645-aea9-23058ac5fd8e)

Then name the group and tick on all the tabs we need.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d3ba1d40-47ba-450c-a88c-fe1a47ffbace)
 
 
Then one new tab is created with the all tabs.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/43b4b972-d231-4d8d-a67a-033d8f476354)

now we need to excute it for that select send group in parallel.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1d591861-f786-4216-b6a1-4dee547e7bca)

Then Send.

IN post request this same only.
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/68460b4a-877e-48af-8684-ad90455e0cdc)

But in GET REQ- Some are getting and other are not.

Here `404 Not Found` 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2a49c63a-8d7e-4592-8979-29052defa694)

But rest ever thing got.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fd7f80bf-4f6f-470e-ad25-58e3a4697c76)

The secret content is `8BHwrf15yEAWSkKzFDI7L6fid76kMQVe`

Now go to Home page and submit the solution.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0ad54a94-e165-4d5f-bfd4-5eb472b844b2)

LAB SOLVED.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9e69dfbe-46ec-483a-b90e-713f51279657)
