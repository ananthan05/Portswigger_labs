## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/206e10d5-4307-4f19-9be3-74602a41604b)

## Solution :
we can see the Admin panel link present.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5c186bb4-33e5-49ae-a0a7-6ebc00a9ee0e)

by clicking it it says access denied.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/cad48514-aebc-45a3-bbf7-e4fe4972ad81)

Send the request to Burp Repeater. 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2294b2ed-46e4-49bd-a7e4-35161f917069)

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as X-Original-URL and X-Rewrite-URL. If a web site uses rigorous front-end controls to restrict access based on URL, but the application allows the URL to be overridden via a request header, then it might be possible to bypass the access controls using a request like the following.

so to acces the admin panel we need to give the payload `X-Original-Url: /admin`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7c79720d-e68d-40fe-b7d0-b6cfc0e9405f)

we got access in admin panel.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8bca3bd2-e282-49d5-9c51-b8dd979fcffc)

now we try to delete carlos.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c4377fa2-5628-4f3d-a9ef-9bca63828d6a)

access denied.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3a445a0d-41b1-49c1-91ac-b9a8d3de736f)

To delete carlos  we need to give the payload `X-Original-Url: /admin/delete` and add `?username=carlos` to the real query string

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/48d567e0-4419-4c58-b88b-82aa1f573c49)

And send this request to orginal.And carlos got deleted we can verfy it by sending admin request again and search `carlos` in that.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2e3c31b4-c54c-409d-8581-b5eb5ff7c7e2)

LAB solved 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f61e26a1-0e12-4357-8af2-4433f4b7dbbf)
