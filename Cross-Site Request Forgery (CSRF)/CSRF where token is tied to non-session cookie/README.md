## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6baffac5-3dcd-4779-8f74-f6cd92e5746d)

## Solution :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f3e87da0-6748-464b-98d3-a95786198a3b)

### Find weak CSRF protection

As usual, the lab application is the blog website. I am again provided with two sets of valid credentials.
I login with the known credentials for `wiener` and change the email address. This results in the following request:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b2ff184e-938f-48cf-a14c-e7fb7f810027)


There are some things expected and other things rather interesting. The session cookie and the csrf-tokens are the expected parts. But there is a second cookie `csrfKey`, that looks very similar to a second session value.

All values remain static for the session. When I logout and login again as the same user, the session cookie changes (this is expected) but csrfKey and csrf-token remain the same.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/dc251ae7-08e5-4bb1-9900-bad443df2a41)


This indicates that the system providing the CSRF protection does not integrate into the session system, but creates its own type of session that is not in sync. This might violate the **tightly connected** property mentioned earlier.

So I check with the second user account. To ensure the sessions do not get mixed up I use the Burp Browser for this. So I login as `carlos`, switch intercept on and change the email address.

The intercepted request I then modify in Burp to contain the session ID from the current `carlos`-session, but both `csrfKey` as well ass `csrf`-token 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/555c0088-53b5-473b-b858-924a21b27846)

Sure enough, the request goes through and carlos email is changed:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c997ef8d-48ca-4124-96e3-9a84f7310bdf)

I can change a victims email with my own CSRF-data. Including the csrf-token in the malicious HTML form is easy, but the `csrfKey` is taken from the cookie. So the next step is to find a way to manipulate the cookie values.

### Manipulate victims cookie

The account page only allows changing of the email, and I can't see a way to use it to manipulate the cookie. So for the first time it is actually due to check the public blog page.

I see two places to input data, the search feature and the `leave a comment` functionality.

The comment feature does not show anything interesting, but when searching something the response looks interesting:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9222d9e9-16c6-41c2-ad7b-c08d21114457)

The search term is reflected into a `LastSearchTerm` cookie. If I can manage to break out of the cookie and set another one, specifically the `csrfKey` cookie, than I have a way to manipulate the cookie value of my victim.

So I put the search term in Repeater to play around.

#### Multiple cookies in one header

The [Set-Cookie docu on mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) states that `To send multiple cookies, multiple Set-Cookie headers should be sent in the same response.`. An interesting detail is the `should` here - perhaps multiple cookies can be set in a single `set-cookie` header even if it is discouraged?

The respective [rfc6265](https://www.rfc-editor.org/rfc/rfc6265#section-3) also contains this should:  `Origin servers SHOULD NOT fold multiple Set-Cookie header fields into a single header field`. 

Looking all the way back to [rfc2109](https://www.rfc-editor.org/rfc/rfc2109) (via the `Obsoletes` links) it shows that this was allowed to have this property: `Informally, the Set-Cookie response header comprises the token Set-Cookie:, followed by a comma-separated list of one or more cookies.`

So I try this out by using `xxx,csrfKey=abc` as search term. Unfortunately, regardless of what encodings I try the browser does ignore this (rightfully so).

#### Inject additional header

The next attempt is now to inject an additional `set-cookie` header with the `csrfKey` data. So I inject a line break into my search term, followed by another `set-cookie` header:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4a615312-75d2-4abb-af92-f31894013239)


And it worked, the server issued two cookie headers. As it was a valid server response containing them, the browser changed the stored cookie to the value choosen by me:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/06e84131-cc2e-4b5d-81a6-da7c588e0bc6)

### Delivery

For delivery one additional hurdle is there: how to force the victim, or its browser, to issue the manipulated search request?

One way is to add this URL as image location. Of course, there will be no image but the request will be made.

So the attack is basically two distinct parts:

1. Update the cookie value to contain my csrfKey value
2. Submit the form with my csrf-token

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6aab038b-3278-42a6-b9e2-a9d16e029197)

**Final payload **

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="https://0a4800d4041e203a80c1808900a400d7.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="pwned&#64;test&#46;com" />
      <input type="hidden" name="csrf" value="A3SRAhW10ulYAujS4LqoGMSAbVtJR1WY" />
      <input type="submit" value="Submit request" />
    </form>
      <img src="https://0a4800d4041e203a80c1808900a400d7.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=DeXLkdkNhCEpCDz5WHWqsRmLrAI6X3wz%3b%20SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```

This is a bit of a race condition, as it relies on the fact that the image request and response are done by the time the auto submit script is executed. I do not know whether there is any parse order that can be relied on. 

So a better way would be to use the `onError` event to submit the form as it enforces the order of first request the picture and process the response and only submit the form once it fails to result in an image. 

For this, the full script part in the image above needs to be removed and `onerror="document.forms[0].submit()"` is added to the img-tag.

After delivering the form to the victim, the lab updates to

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/88555d01-3295-41fb-8552-e273eed81a25)
