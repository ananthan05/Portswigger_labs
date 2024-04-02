## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9a6d7a24-39fa-4e6c-abe9-1fe655186654)

## Solution :

We straightaway see a search functionality.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ae28e86a-da6d-4d49-9380-33679cdc421b)

After performing a search `cyber`, the search term is included on the result page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9b02f581-367d-48ed-bbae-850c711d0567)

>Looking at the page source, the search term displayed is properly encoded. However, it also shows that a javascript takes the search term out of the URL and writes it into an img-tag for some type of tracking. it only show the jave code not what really is happend there.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aacbb995-a249-4234-ac60-a7a66919f288)

>Using the browser tools, I can inspect the resulting HTML. It is visible that my search term is embedded without any apparent safeguards:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9feac5b7-2dc4-463b-bd6b-2bfeff834899)

## Payload

Enter the following simple XSS payload to trigger an alert!

```js
">cyber<script>alert(1)</script>
```

Break out of the img attribute by searching

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c941a6a9-8c81-4016-ba92-a0f00aef5ed5)

it trigger an alert.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/92e0e3b1-a4cf-4208-9f8b-d7e252c45790)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b0b99ad0-c315-4ede-b2c6-5ae29508f126)

## Alternative

The same result can be achieved by injecting anthor payload.

```js
"><svg onload=alert(1)>
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/51d3f80c-2e41-456f-9d80-17a040d8467d)


