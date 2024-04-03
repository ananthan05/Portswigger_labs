## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/725ae8bb-bba6-4b71-9aa4-85462c9925c5)

## Solution :

The lab application is a blog website with search functionality.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/77bc6b13-6d6e-4947-9401-c0fe6380c8df)

First try entering the following simple XSS payload to trigger an alert!

```js
"><script>alert(1)</script>
```
But no pop came.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/240e97dd-a079-4c18-8918-3c66fab8030e)

The innerHTML sink doesn't accept script elements on any modern browser.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1e85bbc4-8c5c-4c94-b922-3cab0073fd16)

> what ever query we are typing stored inside span becuse of innerhtml for bypassing it we will use an alternative elements like `img` or `iframe`. Event handlers such as `onload` and `onerror` can be used in conjunction with these elements.

 XSS payload to trigger an alert!

 ```js
<img src=1 onerror=alert()>
```

> The value of the `src = 1` attribute is invalid and throws an error. This triggers the `onerror` event handler, which then calls the `alert()` function.
> As a result, the payload is executed whenever the user's browser attempts to load the page containing your malicious post.

This raises the alert box.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2aec07e5-1f05-4272-bed6-4473d0842bb2)

The resulting HTML looks like this-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f166264a-6850-4d52-a324-f42869f7cf63)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/933db1a1-6bf1-4023-affc-b35193306fd1)

