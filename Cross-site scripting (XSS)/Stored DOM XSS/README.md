## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/112b223c-fe48-4625-8155-634aa76d5f2e)

## Solution :

We have a functionality to post comments.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/eb34a9b1-abbe-465a-ac2d-dfebab9bd4e5)

First i used normal alert payload for stred xss.

```js
<script>alert()</script>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/abdb125c-3e6f-44c1-920d-75e90d1fc716)

alert did not came.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a0ddb494-6010-484b-adad-d4dbfcb62407)

HTML code -

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6c33610b-9962-4de7-bbea-8f4d01736804)


>The comments are not sent by the server directly with the response, but dynamically loaded and displayed via JavaScript:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/93047ba5-3ffb-4c8c-8393-61f3d3232b7a)

So the natural next step is to check that JavaScript. Some things become obvious:

The content of the elements are added as `innerHTML`, which is vulnerable to injections (innerText would be better here)

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a10a29a7-882c-4bd2-a420-309c0ae0e817)

we need come out of the `<p> script </p>`. for that we will use `<>` how out of that our scrpit will have this in front.

Payload.

```js
<><img src=1 onerror=alert()>
```
>In an attempt to prevent XSS, the website uses the JavaScript replace() function to encode angle brackets. However, when the first argument is a string, the function only replaces the first occurrence. We exploit this vulnerability by simply including an extra set of angle brackets at the beginning of the comment. These angle brackets will be encoded, but any subsequent angle brackets will be unaffected, enabling us to effectively bypass the filter and inject HTML.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aff32952-7ef3-45ca-85dd-09cde781bbee)

This payload will triger an alert-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d112f6f9-6817-42dd-8c4c-d8be5e78a55e)

HTML code-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c091b42a-92bb-48b1-9468-76e9b6f670c8)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5cdec911-4437-423b-8bdd-f7b118335261)


