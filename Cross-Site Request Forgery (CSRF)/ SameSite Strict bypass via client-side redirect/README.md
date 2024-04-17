## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/74533a62-b999-4ff7-8b41-fc739672d505)

## Solution :

the `POST /my-account/change-email` request and notice that this doesn't contain any unpredictable tokens, so may be vulnerable to CSRF if you can bypass any SameSite cookie restrictions.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/05f49747-7798-4026-9f8a-ccc14e3d31a5)

Look at the response to your `POST /login` request. Notice that the website explicitly specifies `SameSite=Strict` when setting session cookies. This prevents the browser from including these cookies in cross-site requests.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/70c35394-b004-4e2f-b3f2-e7f9b535782c)

## Identify a suitable gadget

In the browser, go to one of the blog posts and post an arbitrary comment. Observe that you're initially sent to a confirmation page at `/post/comment/confirmation?postId=x` but, after a few seconds, you're taken back to the blog post.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b7d3ad24-ea80-4387-98db-61561ca3d3b6)

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2095174c-5154-497c-91cf-ac1472a44bab)

> Study the JavaScript and notice that this uses the postId query parameter to dynamically construct the path for the client-side redirect.

In the proxy history, right-click on the GET `/post/comment/confirmation?postId=9` request and select Copy URL.And Try injecting a `path traversal` sequence so that the dynamically constructed redirect URL will point to your account page:

```
/post/comment/confirmation?postId=9/../../my-account
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5938c6d6-220d-4629-9be1-2147fc3792ab)

Observe that the browser normalizes this URL and successfully takes you to your account page. This confirms that you can use the `postId` parameter to elicit a GET request for an arbitrary endpoint on the target site.

## Bypass the SameSite restrictions

In the browser, go to the exploit server and create a script that induces the viewer's browser to send the GET request you just tested. The following is one possible approach:

```html
<script>
    document.location = "https://0a040032041a40b885a86270005e0019.web-security-academy.net/post/comment/confirmation?postId=../my-account";
</script>
```
Store and view the exploit yourself.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bfcb652f-d2b0-4de5-a32d-3a4550909c8a)


Observe that when the client-side redirect takes place, you still end up on your logged-in account page. This confirms that the browser included your authenticated session cookie in the second request, even though the initial comment-submission request was initiated from an arbitrary external site.

Craft an exploit-

In Burp Repeater `POST /my-account/change-email` request  Change request method. Burp automatically generates an equivalent GET request.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/277bd157-b1c0-4496-888a-db734f82ab86)

Observe that the endpoint allows you to change your email address using a GET request.

Go back to the exploit server and change the `postId` parameter in your exploit so that the redirect causes the browser to send the equivalent `GET` request for changing your email address:

```html
<script>
    document.location = "https://0a040032041a40b885a86270005e0019.web-security-academy.net/post/comment/confirmation?postId=../my-account/change-email?email=cyber7%40gmail.com%26submit=1";
</script>
```
> Note that you need to include the submit parameter and URL encode the ampersand delimiter to avoid breaking out of the postId parameter in the initial setup request.

Deliver the exploit to the victim. After a few seconds, the lab is solved-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/74026793-49eb-490a-916d-7c79dff15512)

