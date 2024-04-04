## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c6df8521-8608-499c-a6cc-a66490c218a8)

## Solution :

Clicking on the `Submit feedback` link on the main page of the blog leads to the path `/feedback?returnPath=/`.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/44dd01a7-903b-4107-8003-7922cb14e0ed)

`back` link has vulnerablity the resulting HTML-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/64c89ae3-394f-451b-9133-4d6b6a23da15)

> If a JavaScript library such as jQuery is being used, look out for sinks that can alter DOM elements on the page. For instance, jQuery's attr() function can change the attributes of DOM elements. If data is read from a user-controlled source like the URL, then passed to the attr() function, then it may be possible to manipulate the value sent to cause XSS.
> You can exploit this by modifying the URL so that the location.search source contains a malicious JavaScript URL. After the page's JavaScript applies this malicious URL to the back link's href, clicking on the back link will execute it.

payload to trigger an alert!

```js
javascript:alert(document.cookie)
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f3063756-96de-4490-9183-62ee88e73929)

Then press back to triger the alert.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/753572f8-568a-4f80-bc38-5861447663cb)

LAB Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b6ec139b-1415-4fe5-b1d6-0b15470f462c)

