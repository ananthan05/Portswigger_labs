## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/95eb6209-b662-471c-8045-04d9eb9dcc60)

## Solution :

Log in using the admin credentials.using `administrator:admin`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1c62c123-eba0-4a10-ab2f-3ac28898bc94)

Browse to the admin panel, promote carlos.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9d716f94-bc84-4a4a-b803-db2d3939c0a4)

Send this request to repeater.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/05b3e958-bd44-4439-89d3-40c6645c0c1f)

NOW log in with the non-admin credentials `wiener:peter`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/978f6050-1b73-4891-bb85-1bd4b1835a6e)

So now we can try logging in as wiener using the credentials given & try to promote ourselves as administrator.

With thehelp of inspect element , we grab the cookie of wiener.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b11a07a3-8679-4dc7-b23a-5eb62e2ad87a)

Cookie of wiener -`RZVTsg4AYQ71Mc6P1KQWCRU6Uq2ROjt7`

Let send the non admin request with the admin's session cookie.

we try to upgrade ourself(wiener) by changing the cookie value of admin to non admin in the request -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3e0f3605-b1de-482b-9055-b641161127d2)

We can see that it has a referrer header which points to /admin.

> Some websites **base access controls on the Referer header submitted in the HTTP reques**t. The Referer header is generally added to requests by browsers to indicate the page from which a request was initiated.
>
> For example, suppose an application robustly enforces access control over the main administrative page at **/admin**, but for sub-pages such as **/admin/deleteUser** only inspects the Referer header. If the 
> Referer 
> header contains the main **/admin** URL, **then the request is allowed**.
> 
> In this situation, since the Referer header can be fully controlled by an attacker, they can forge direct requests to sensitive sub-pages, supplying the required Referer header, and so gain unauthorized access. 

LAB Solved.


if we are sending the request Without /admin in referrer header

We will get 401 - Unauthorized

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fc73855f-6127-4962-ba91-82052b93304d)
