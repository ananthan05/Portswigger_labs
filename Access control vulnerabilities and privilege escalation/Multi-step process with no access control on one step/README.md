## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/adbe7e52-2619-46a6-bee1-15175e33c180)

## Solution :

Log in using the admin credentials.using `administrator:admin`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bac6e811-538c-4902-ae73-fe24456b0a30)

Browse to the admin panel, promote carlos.

Step 1 in the process -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b7d51184-fa4d-43e1-8b1c-71efde25f1d7)

Send this request to repeater.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c34ec7a5-de51-495c-a4c5-40d3f2348312)


Here we upgreaded privileges of carlos.

After modifying the privileges, we get a page like this & where the request contains a additional parameter called confirmned=true,

Step 2 in the process -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e353ccfd-4fdc-4f88-a4bb-9329ec892a03)

Send this request to repeater.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c09ca4c7-5c66-4d4e-833e-7990dd878f44)

This process of upgrading/downgrading a user's privileges has 2 steps that's why this is a multi step process.


We here have the admin's cookie which we can send the same request but with non admin cookie.

Here note that we have a parameter called confirmed=true/false in the POST request body which takes us to /admin .

log in with the non-admin credentials `wiener:peter`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/377476d9-3b2d-4c88-acb1-5bd833fd1647)

So now we can try logging in as wiener using the credentials given & try to promote ourselves as administrator.

With thehelp of inspect element , we grab the cookie of wiener.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a3ee928a-316f-4737-a909-a2ef9073058e)


Cookie of wiener -`SZbuFSlPCgU3E85etHK9qcDSbNeudtlJ`


Let send the non admin request with the admin's session cookie.

If we try to upgrade ourself(wiener) by changing the cookie value of admin to non admin in the request of first step , we get 401 - UNAUTHORIZED

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/97a7de27-53e8-4077-93e6-29e53abc8517)


But , if we try the same process in the second step ie - Confirming the action step, we get a `302 - Redirect' which means we bypassed the acces control measure & upgraded the privilege of ourselves.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b4005793-3352-474f-b2e2-0a1a08759260)

solved the lab.
