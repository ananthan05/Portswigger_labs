## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0277ad5b-a264-4089-8687-a13f3d94c4ac)

## Solution :

Click a Product and Check out the Stock Checking Functionality

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/be8c7433-6a5d-427b-bc62-f25db7add91c)

Capture the request, you can see that there is a parameter called stockAPI which has a encoded string.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/eba9aaeb-f9f5-48c8-a446-2b6d0c32c8ca)

Send the request to the decoder and click smart decode to decode the string and know that it is directing to an internal page

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4270e3cc-bebf-4313-a3e0-5d5c7ef463d5)

So now, change the stockAPI parameter to `http://localhost/admin` as given in Lab description and send the request

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bd790fd8-fb87-4c13-a6f2-c2a254a11782)

WE got the admin acess.

Now you can able to see that the response is successful and on inspecting the code you can get the URL to delete user Carlos

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/93a0dd10-7bbb-4e15-ae0a-b65b65bb1298)

Copy the URL that we found on 4th step’s response.Now Paste it on the stockAPI Parameter.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c5f3350c-8399-4761-8715-dccc4648d672)

LAB SOlved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5d785250-a867-4440-ae1b-bc23f839ced2)
