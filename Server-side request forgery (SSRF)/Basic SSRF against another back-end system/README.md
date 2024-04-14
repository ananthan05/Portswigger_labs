## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/579bf9da-b968-46c7-a3d5-a05779ceeb8f)

## Solution :

Click a Product and Check out the Stock Checking Functionality

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/922960bd-1bc5-4d1a-ac32-5c308095edce)

Capture the request, you can see that there is a parameter called stockAPI which has a encoded string.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d0fc700a-5558-4569-989f-073ebffd8362)

Press `control+SHIFT+U` to encode the url.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/abd1b69b-8c76-4117-a2f8-e8e821166b81)

intercept the request in Burp Suite, and send it to Burp Intruder.And Click "Clear §", change the stockApi parameter to http://192.168.0.1:8080/admin then highlight the final octet of the IP address (the number 1), click "Add §".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4a2b06dd-e9d9-4ff3-901f-685272459167)

Switch to the Payloads tab, change the payload type to Numbers, and enter 1, 255, and 1 in the "From" and "To" and "Step" boxes respectively..

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5278081d-2d38-4bad-b572-6cf940c07a92)

Click "Start attack".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bab760f6-076e-4cb3-88a7-6544da4fac60)

Click on this request, send it to Burp Repeater, and change the path in the stockApi to: `/admin/delete?username=carlos`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/790d7512-c600-4b67-8f06-d3de6e3f6a41)

delete the user carlos and lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4f2bd72c-ff9f-46fd-9cbb-79c9eee13f5b)
