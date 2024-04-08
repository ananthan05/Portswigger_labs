# Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a66be3e0-1c67-4cab-91a9-6ad8073fc19c)

## Solution :

> List of allowed characters

> Complete List of chracters: / < > \ ‘ “ = ; * & \` ( ) , { }

>Allowed inside Javascript URL : / < > \ ‘ “ = ; * & \` , { }

>List of Blocked Characters: ()

First, we need to find the source from which we can give input, and then we need to identify where our input is reflected.

So After some searching, it is identified that the Post URL is reflected in the Back to Blog anchor tag as given in the below screenshot.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/93c6db5b-9911-49dd-9ed5-4aa1a3c0bd24)

URL Based XSS in `javascript:fetch()`

Code-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/37036094-2cd7-430a-a291-790ce3041270)

if we add a random character after `2` then it will change our `postId` parameter so we need to add `&` to remain postId untouched.


![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6ac07470-f1ba-4a3b-8f46-3041fc70c792)

So now we have to inject javascript code in `fetch()` without breaking our javascript.

So our payload will be.

```js
&'}
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1220136f-10d1-45da-8b6c-f8028aad8681)

so, now in fetch API code, the second parameter will be completed, `{method: …… ’}`

now we can inject our code using `,` which will be treated as a fetch API parameter. So our payload will be.

```js
&'},
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8d69dbf0-a0ed-49ac-a606-60dec38a433b)

We have to call the alert function but after a certain try, it is clear that `()` is blocked. so we need to call the alert function with `1337` as a parameter without using `()`.

So we can easily use toString override method of window object. So when we write,`window+''`

It will try to run toString method on window object.

So let’s make our own function which will run when toString is called.
```js
f=x=>{throw/**/onerror=alert,1337}
```
or

```js
f=x=>{{onerror=alert}throw/**/1337}
```
>In the above function, we need to assign an alert in onerror. so whenever onerror will be called it will call alert. and we are passing argument using throw.

>`/**/` will be used because space is not allowed. and in javascript when we write throw a,2,3 it will be the same as throw 3. a,2 are ignored so we can use this to write onerror=alert line.

>And to assign in toString we can write toString=f.

Now after combining all the pieces to gather our final payload will be.

```js
&'},f=x=>{throw/**/onerror=alert,1337},toString=f,window+''
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/04cb4964-fbf1-49f7-910a-06b7dda504e2)

HTML-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/19093f26-b96b-4693-a2d5-4c32dd28e294)

after pressing the `Back to Blog` alert did not came.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/910e731d-baa5-420a-a739-9850d7b800ac)

now our injected code will not break javascript for that we need to match `‘}` which will be added after our injected code. so now as per the syntax we can add `{x:‘` .

so the final payload will be

```js
&'},f=x=>{throw/**/onerror=alert,1337},toString=f,window+'',{x:'
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f5c350de-840d-415a-90e6-eeae47fcb799)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/afe443e3-e5c1-4339-a68f-d2aaf354c4e5)


Now go and  press the `Back to Blog` alert will pop up.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/239cb2b9-d7a1-4e59-a9d7-280de584efec)

HTML-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/973652ca-60cc-4058-b0b3-ca6b5b3ac4ba)


## An alternative payload

```js
&'},x=z=>{x=new/**/DOMMatrix;matrix=alert;x.a=1337;location='javascript'+':'+x},toString=x,window+'',{x:'
```

click `“Back to blog”` link to pop alert message box and solve the lab.
