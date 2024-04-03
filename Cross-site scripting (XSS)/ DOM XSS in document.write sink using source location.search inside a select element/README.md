## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b1b771b7-c603-4a6b-98a4-e0a0fabd4fa7)

## Solution :

>The lab application is again the shop website containing the stock check feature. This time, the selection box for it is created dynamically by client side JavaScript. The defining feature that requires this is that if a store ID is provided in the URL, the store is pre-selected. For example, adding `&storeId=paris` to the URL will put Milan in first place of the list and selects it:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b2124d31-4494-4293-8764-8061d54ab934)

This is done by this Java script-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3b9cfc57-124e-4055-9aac-0cf6e02165a5)

HTML looks like this-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f6c06072-74ef-4add-ad83-90cfa6590d58)

> I can not directly add some JavaScript in the text of the option tag. But I can complete the tags and put script content outside of the scope of the option.

 Payload to script to get the  content outside 

```
&storeId=Paris</option>we can script here 
```

The resulting HTML looks like this-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3870b3cb-c99a-40a8-b5d6-6ce18a2572ee)

The location of the `we can script here` is just a right spot for adding a script.

Modifying the URL to use-

The Payload is-

```js
&storeId=Paris</option><script>alert(1)</script>
```

This raises the alert box.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3f8bb4ab-1438-49dc-9b41-68dfa422bf5f)

The resulting HTML looks like this-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/26a7bfc6-496f-4970-8ea2-ffcc97170c77)

LAB solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a81fc851-68ad-48b2-93d6-f1ed700df0fa)

